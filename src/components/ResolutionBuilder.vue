<template>
    <div>
        <form
            @submit.prevent="generate"
            @reset.prevent="reset"
        >
            <div class="md:flex">
                <div class="form-group md:mr-2 md:w-1/2">
                    <label
                        class="label"
                        for="x-aspect-field"
                    >
                        X Aspect Ratio
                    </label>
                    <input
                        id="x-aspect-field"
                        class="input"
                        type="number"
                        v-model.number="form_data.xAspect"
                    >
                </div>

                <div class="form-group md:ml-2 md:w-1/2">
                    <label
                        class="label"
                        for="y-aspect-field"
                    >
                        Y Aspect Ratio
                    </label>
                    <input
                        id="y-aspect-field"
                        class="input"
                        type="number"
                        v-model.number="form_data.yAspect"
                    >
                </div>
            </div>

            <div class="md:flex">
                <div class="form-group md:mr-2 md:w-1/2">
                    <label
                        class="label"
                        for="division-field"
                    >
                        Divisible By
                    </label>
                    <input
                        id="division-field"
                        class="input"
                        type="number"
                        v-model.number="form_data.divisibleBy"
                    >
                </div>

                <div class="form-group md:ml-2 md:w-1/2">
                    <label
                        class="label"
                        for="max-results-field"
                    >
                        Max Results
                    </label>
                    <input
                        id="max-results-field"
                        class="input"
                        type="number"
                        v-model.number="form_data.maxMultiple"
                    >
                </div>
            </div>

            <div class="mt-5">
                <div class="inline-block mr-5">
                    <label
                        class="label"
                        for="division-checkbox"
                    >
                        Only show divisible rows
                    </label>
                    <input
                        id="division-checkbox"
                        class="ml-2"
                        type="checkbox"
                        v-model="form_data.showOnlyDivisible"
                    >
                </div>

                <button
                    class="button"
                    type="reset"
                >
                    Reset
                </button>

                <button
                    class="button primary"
                    type="submit"
                >
                    Generate
                </button>
            </div>
        </form>

        <h2 class="font-light text-2xl mt-5">Generated Resolutions</h2>
        <table class="custom-table">
            <thead>
                <tr>
                    <th class="w-8"></th>
                    <th>Width</th>
                    <th>Height</th>
                    <th>Divisible by {{ form_data.divisibleBy }}</th>
                </tr>
            </thead>

            <tbody>
                <tr
                    v-for="(row, index) in list"
                    :key="index"
                    :class="{
                        'even': index % 2 === 0,
                        'odd': index % 2 === 1,
                        'highlight': listRowDivisibleBy(row),
                    }"
                >
                    <td>{{ index +1 }}</td>
                    <td>{{ row.width }}</td>
                    <td>{{ row.height }}</td>
                    <td>{{ listRowDivisibleBy(row) ? 'Yes' : 'No' }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                form_data: null,
                list: [],
            }
        },

        created() {
            this.reset();
        },

        methods: {
            reset() {
                this.form_data = {
                    xAspect: 16,
                    yAspect: 9,
                    divisibleBy: 8,
                    maxMultiple: 10,
                    showOnlyDivisible: false,
                }

                this.generate();
            },
            generate() {
                this.list = [];

                for (let multiple = 1; this.list.length < this.form_data.maxMultiple; multiple++) {
                    const newRow = {
                        width: this.form_data.xAspect * multiple,
                        height: this.form_data.yAspect * multiple,
                    };

                    if (! this.form_data.showOnlyDivisible
                        || this.form_data.showOnlyDivisible && this.listRowDivisibleBy(newRow)
                    ) {
                        this.list.push(newRow);
                    }
                }
            },
            listRowDivisibleBy(row) {
                return row.width % this.form_data.divisibleBy === 0
                    && row.height % this.form_data.divisibleBy === 0;
            }
        }
    }
</script>
