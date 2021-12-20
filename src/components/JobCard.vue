<template>
    <div class="jobs">
        <div
            class="d-md-flex justify-content-between container shadow rounded py-3 px-4 bg-white"
            id="job"
            :class="jobs.featured ? 'border-left' : ''"
        >
            <div class="d-flex align-items-center gap-4">
                <img :src="require('@/assets/' + jobs.logo)" height="65vh" />

                <div>
                    <!-- company info -->
                    <div class="d-flex gap-2 mb-1 align-items-center">
                        <p class="mb-0 fw-bold small teal">{{ jobs.company }}</p>

                        <p v-if="jobs.new" class="badge alert-primary small mb-0 fw-normal">NEW!</p>

                        <p v-if="jobs.featured" class="badge alert-dark small mb-0 fw-normal">
                            FEATURED
                        </p>
                    </div>

                    <!-- position -->
                    <div>
                        <h6 class="my-2 fw-bold">{{ jobs.position }}</h6>
                    </div>

                    <!-- job info -->
                    <div class="d-flex gap-2 text-muted small">
                        <p class="mb-0">{{ jobs.postedAt }}</p>
                        ∙
                        <p class="mb-0">{{ jobs.contract }}</p>
                        ∙
                        <p class="mb-0">{{ jobs.location }}</p>
                    </div>
                </div>
            </div>

            <!-- tags -->

            <!-- linebreak  -->
            <hr size="3" />

            <div class="d-flex gap-3 align-items-center">
                <div v-for="tag in tags" v-bind:key="tag">
                    <button type="button" class="btn btn-light btn-sm fw-bold teal">
                        {{ tag }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "JobCard",
    props: {
        jobs: {
            id: Number,
            company: String,
            logo: String,
            new: Boolean,
            featured: Boolean,
            position: String,
            role: String,
            level: String,
            postedAt: String,
            contract: String,
            location: String,
            languages: Array,
            tools: Array,
        },
    },

    data() {
        return {
            tags: [],
        };
    },

    beforeMount() {
        this.$nextTick(function () {
            // console.log("this is the image:", this.jobs.logo.trim());

            this.jobImage = this.jobs.logo;

            //combine arrays into 1
            this.tags = this.jobs.languages.concat(this.jobs.tools);

            console.log(this.tags);
        });
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* TODO: add styles  */

.teal {
    color: hsl(180, 29%, 50%);
}

.alert-primary {
    color: white;
    background: hsl(180, 29%, 50%);
}

.alert-dark {
    color: white;
    background: black;
}

.border-left {
    border-left: 6px solid hsl(180, 29%, 50%);
}

#job:hover {
    transform: scale(1.03);
    cursor: pointer;
}
</style>
