<template>
    <div class="container">
        <h1>Percentage from<br />52-week High</h1>
        <div class="content">
            <div v-if="items.length > 1">
                <table>
                    <thead>
                        <tr>
                            <th>Stock</th>
                            <th>Current Price</th>
                            <th>52-Week High</th>
                            <th>% from 52-Week High</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in items" :key="item.name">
                            <td><strong>{{ item.name }}</strong></td>
                            <td>{{ item.c }}</td>
                            <td>{{ item.high52 }}</td>
                            <td :style="{ backgroundColor: getColor(item.percentageFrom52WeekHigh) }">
                                {{ item.percentageFrom52WeekHigh }}%
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div v-else>
                <InitPercentageFromHigh />
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    items: {
        type: Array,
        default: () => []
    }
})

const getColor = (percentage) => {
    if (percentage > 10) {
        return '#32D732'; // 강한 상승 (> 10%)
    } else if (percentage > 5) {
        return '#28ac28'; // 상승 (5% ~ 10%)
    } else if (percentage > 3) {
        return '#1e811e'; // 상승 (3% ~ 5%)
    } else if (percentage > 0) {
        return '#145614'; // 미세 상승 (0% ~ 3%)
    } else if (percentage === 0) {
        return '#051505'; // 동일 (0%)
    } else if (percentage < -10) {
        return '#d73232'; // 강한 하락 (< -10%)
    } else if (percentage < -5) {
        return '#ac2828'; // 하락 (-5% ~ -10%)
    } else if (percentage < -3) {
        return '#811e1e'; // 하락 (-3% ~ -5%)
    } else if (percentage < 0) {
        return '#561414'; // 미세 하락 (0% ~ -3%)
    }
}
</script>

<style scoped>
h1,
h2 {
    color: #F08;
}

.container {
    display: block;
    justify-content: center;
    position: relative;
    border-right: 2px solid #666;
}

.content {
    overflow-x: hidden;
    margin: 0 10px 0 0;
    border-collapse: separate;
    border-spacing: 0;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
}

table {
    width: 100%;
    border-radius: 10px;
    text-align: left;
}

th,
td {
    padding: 15px;
    border-bottom: 2px solid #eaeaea;
    max-width: 30px;
}

th {
    background-color: #3f3f3f;
    /* 고급스러운 어두운 파란색 */
    color: #ffffff;
    font-weight: 600;
    text-align: left;
    font-size: 16px;
    line-height: 20px;
}

td {
    font-size: 15px;
    font-weight: bold;
    color: #ddd;
}

tbody tr:hover {
    background-color: #1f1f1f;
    /* 마우스 호버 시 */
}

strong {
    font-weight: bold;
    color: #32D732;
    /* 주식 이름 색상 */
}

td:last-child {
    text-align: right;
    /* 퍼센트 변동값 오른쪽 정렬 */
}

/* 중간 크기 화면 (태블릿)에서의 스타일링 */
@media (min-width: 768px) and (max-width: 1279px) {

    th,
    td {
        padding: 10px;
        font-size: 12.5px;
    }

    th {
        text-align: center;
    }

    .content {
        border-right: 0;
    }
}

@media all and (max-width: 767px) {
    .container {
        margin-top: 30px;
        border-right: 0;
    }

    .content {
        margin: 20px 20px 10px 0;
        border-right: 0;
    }

    th,
    td {
        font-size: 12px;
    }
}
</style>