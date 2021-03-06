<template>
  <v-navigation-drawer v-model="showCreateEdit" app clipped right width="500">
    <template v-slot:prepend>
      <v-list-item two-line>
        <v-list-item-content>
          <v-list-item-title v-if="id" class="title">Edit</v-list-item-title>
          <v-list-item-title v-else class="title">New</v-list-item-title>
          <v-list-item-subtitle>Application</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </template>
    <ValidationObserver>
      <v-card slot-scope="{ invalid, validated }" flat>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12>
                <span class="subtitle-2">Details</span>
              </v-flex>
              <v-flex xs12>
                <ValidationProvider name="name" rules="required" immediate>
                  <v-text-field
                    v-model="name"
                    slot-scope="{ errors, valid }"
                    :error-messages="errors"
                    :success="valid"
                    label="name"
                    hint="a name for your application."
                    clearable
                    required
                  />
                </ValidationProvider>
              </v-flex>
              <v-flex xs12>
                <ValidationProvider name="source" rules="required" immediate>
                  <v-text-field
                    v-model="source"
                    slot-scope="{ errors, valid }"
                    :error-messages="errors"
                    :success="valid"
                    label="Source"
                    hint="Application's source."
                    clearable
                    required
                  />
                </ValidationProvider>
              </v-flex>
              <v-flex xs12>
                <ValidationProvider name="uri" rules="required" immediate>
                  <v-text-field
                    v-model="uri"
                    slot-scope="{ errors, valid }"
                    :error-messages="errors"
                    :success="valid"
                    label="URI"
                    hint="Application's URI."
                    clearable
                    required
                  />
                </ValidationProvider>
              </v-flex>
              <v-flex xs12>
                <ValidationProvider name="description" immediate>
                  <v-textarea
                    v-model="description"
                    slot-scope="{ errors, valid }"
                    label="Description"
                    :error-messages="errors"
                    :success="valid"
                    hint="The application's description."
                    clearable
                    required
                  />
                </ValidationProvider>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="secondary" @click="closeCreateEdit()">Cancel</v-btn>
          <v-btn
            color="primary"
            :loading="loading"
            :disabled="invalid || !validated"
            @click="save()"
          >Save</v-btn>
        </v-card-actions>
      </v-card>
    </ValidationObserver>
  </v-navigation-drawer>
</template>

<script>
import { mapFields } from "vuex-map-fields"
import { mapActions } from "vuex"
import { ValidationObserver, ValidationProvider } from "vee-validate"
export default {
  name: "ApplicationNewEditSheet",

  components: {
    ValidationObserver,
    ValidationProvider
  },

  computed: {
    ...mapFields("application", [
      "selected.name",
      "selected.id",
      "selected.uri",
      "selected.description",
      "selected.source",
      "selected.loading",
      "dialogs.showCreateEdit"
    ])
  },

  methods: {
    ...mapActions("application", ["save", "closeCreateEdit"])
  }
}
</script>
