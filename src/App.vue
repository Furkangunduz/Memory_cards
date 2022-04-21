<template>
    <div>
        <h3>Tried {{ tried }} times</h3>
        <h4>Score : {{ score }}</h4>
        <div class="container">
            <div v-for="(col, colindx) in Words" :key="colindx">
                <button
                    @click="makeActive"
                    :disabled="isDisable"
                    v-for="(row, rowindx) in col"
                    :key="rowindx"
                    class="card"
                >
                    <div class="front"></div>
                    <div class="back">{{ row }}</div>
                </button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    components: {},
    data() {
        return {
            Words: [
                ["elma", "kaysı", "havuc", "armut"],
                ["karpuz", "şeftali", "armut", "elma"],
                ["domates", "karpuz", "kiraz", "şeftali"],
                ["kaysı", "kiraz", "domates", "havuc"],
            ],
            tried: 0,
            score: 0,
            activeCount: 0,
            isDisable: false,
        };
    },
    methods: {
        makeActive(e) {
            if (!this.isDisable) {
                e.target.classList.add("active");
                this.activeCount++;
            }

            if (this.activeCount == 2) {
                this.tried++;
                this.isDisable = true;
                var active = document.querySelectorAll(".active");
                var firstSelectedCard =
                    active[0].querySelector(".back").innerHTML;
                var secondSelectedCard =
                    active[1].querySelector(".back").innerHTML;

                setTimeout(() => {
                    if (firstSelectedCard == secondSelectedCard) {
                        this.score++;
                        active.forEach((e) => {
                            e.style.visibility = "hidden";
                        });
                    } else {
                        active.forEach((e) => {
                            e.classList.remove("active");
                        });
                    }
                    this.activeCount = 0;
                    this.isDisable = false;
                }, 750);
            }
        },
    },
};
</script>
