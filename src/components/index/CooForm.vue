<template>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
            <q-input class="new-coo" bottom-slots v-model="newCooText" placeholder="Podziel się czymś ciekawym."
                counter maxlength="280" autogrow>
                <template v-slot:before>
                    <q-avatar size="4em" class="gt-sm">
                        <img :src="userStore.loggedUser.avatarUrl">
                    </q-avatar>
                </template>
            </q-input>
        </div>
        <div class="col col-shrink">
            <q-btn unelevated rounded color="primary" label="Gruchnij" no-caps :disable="!newCooText" class="q-mb-lg"
                @click="addNewCoo" />
        </div>
    </div>
</template>

<script>
import {ref} from 'vue'
import { useUserDataStore } from 'src/stores/user-data-store';
export default {
    name: 'CooForm',
    setup(_, {emit}){
        const userStore = useUserDataStore();
        const newCooText = ref('');

        const addNewCoo = () => {
            emit('addClicked', {cooText: newCooText.value})
            newCooText.value = "";
        }

        return {
            newCooText,
            addNewCoo,
            userStore
        }
    }
}
</script>

<style lang="sass">
.new-coo
  textarea
    font-size: 19px
    line-height: 1.4 !important
</style>