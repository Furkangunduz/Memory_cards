<template>
    <div class="container">
        <div>
            <div v-for="(col, colindx) in Words" :key="colindx">
                <div
                    @click="makeActive"
                    v-for="(row, rowindx) in col"
                    :key="rowindx"
                    class="card"
                >
                    <div class="front"></div>
                    <div class="back">{{ row }}</div>
                </div>
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
                ["kaysı", "kiraz", "domates", "havuz"],
            ],
            activeCount: 0,
        };
    },
    methods: {
        makeActive(e) {
            e.target.classList.add("active");
            this.activeCount++;

            console.log(this.activeCount);
            if (this.activeCount == 2) {
                var active = document.querySelectorAll(".active");
                var firstSelectedCard =
                    active[0].querySelector(".back").innerHTML;
                var secondSelectedCard =
                    active[1].querySelector(".back").innerHTML;

                if (firstSelectedCard == secondSelectedCard) {
                    console.log("score++");
                }
                setTimeout(() => {
                    active.forEach((e) => {
                        e.classList.remove("active");
                    });
                    this.activeCount = 0;
                }, 500);
            }
        },
    },
};
</script>
