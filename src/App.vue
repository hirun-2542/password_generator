<script setup>
import { ref, computed } from "vue";

const lowerCase = ref(true);
const upperCase = ref(null);
const number = ref(null);
const specialChars = ref(null);
const length = ref(10);
const refreshpassword = ref(false);

const generatePassword = computed(() => {
    refreshpassword.value;
    const lower = "abcdefghijklmnopqrstuvwxyz";
    const upper = lower.toUpperCase();
    const num = "0123456789";
    const special = "!@#$%&'()*+,^-./:;<=>?[]_`{~}|";
    let retVal = "";
    let charset = "";
    if (lowerCase.value) {
        charset += lower;
    }
    if (upperCase.value) {
        charset += upper;
    }
    if (number.value) {
        charset += num;
    }
    if (specialChars.value) {
        charset += special;
    }
    for (let i = 0, n = charset.length; i < length.value; ++i) {
        retVal += charset.charAt(Math.floor(Math.random() * n));
    }
    return retVal;
});

const addOperator = (operator) => {
    if (operator === "+") {
        if (length.value < 50) {
            length.value++;
        }
    } else if (operator === "-") {
        if (length.value > 1) {
            length.value--;
        }
    }
};

const showmore = computed(() => {
    if (generatePassword.value.length > 20) {
        return generatePassword.value.slice(0, 20) + "...";
    } else {
        return generatePassword.value;
    }
});

const security = computed(() => {
    if (generatePassword.value.length > 12) {
        return "Very Strong";
    } else if (generatePassword.value.length > 10) {
        return "Strong";
    } else if (generatePassword.value.length > 7) {
        return "Good";
    } else if (generatePassword.value.length > 4) {
        return "Weak";
    } else {
        return "Very Weak";
    }
});

const secureColor = computed(() => {
    if (generatePassword.value.length > 12) {
        return "badge veryStrong";
    } else if (generatePassword.value.length > 10) {
        return "badge strong";
    } else if (generatePassword.value.length > 7) {
        return "badge good";
    } else if (generatePassword.value.length > 4) {
        return "badge weak";
    } else {
        return "badge weak";
    }
});
</script>

<template>
    <div class="generator">
        <h1>Random Password Generator</h1>
        <div class="input-content">
            <div class="generator-input">
                <div class="password">{{ showmore }}</div>
                <span :class="secureColor">{{ security }}</span>
                <div
                    class="generator-icon"
                    @click="refreshpassword = !refreshpassword"
                ></div>
            </div>
        </div>
        <div class="generator-settings">
            <div class="length-setting">
                <label class="length" for="length"
                    >Password Length :
                    <span style="color: #0070f6">{{ length }}</span>
                </label>
                <button class="btn-circle" @click="addOperator('-')">
                    <img
                        src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0iIzA3MUQyQiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8cGF0aCBkPSJNMTguNTU1OSAxMi4wMjE1SDUuOTE4NDYiIHN0cm9rZT0iIzA3MUQyQiIgc3Ryb2tlLXdpZHRoPSIxLjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIvPgo8L3N2Zz4K"
                        alt=""
                    />
                </button>
                <div>
                    <input
                        class="slider"
                        type="range"
                        min="1"
                        max="50"
                        v-model="length"
                    />
                </div>
                <button class="btn-circle" @click="addOperator('+')">
                    <img
                        src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0iIzA3MUQyQiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8cGF0aCBkPSJNMjAuMTgyOSAxMS45OTg2SDEyLjAwNzlNMTIuMDA3OSAxMS45OTg2VjIwLjE3MzVNMTIuMDA3OSAxMS45OTg2SDMuODcwNDhNMTIuMDA3OSAxMS45OTg2VjMuODYxMDgiIHN0cm9rZT0iIzA3MUQyQiIgc3Ryb2tlLXdpZHRoPSIxLjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIvPgo8L3N2Zz4K"
                        alt=""
                    />
                </button>
            </div>
            <div class="char-set">
                <label class="option" for="option"> Characters used : </label>
                <input
                    class="lower"
                    type="checkbox"
                    id="lowerCase"
                    v-model="lowerCase"
                />
                <label class="lower" for="lowerCase">a-z</label>
                <input
                    class="upper"
                    type="checkbox"
                    id="upperCase"
                    v-model="upperCase"
                />
                <label class="upper" for="upperCase">A-Z</label>
                <input
                    class="number"
                    type="checkbox"
                    id="number"
                    v-model="number"
                />
                <label class="number" for="number">0-9</label>
                <input
                    type="checkbox"
                    id="specialChars"
                    v-model="specialChars"
                />
                <label for="specialChars">#$&</label>
            </div>
        </div>
    </div>
</template>

<style scoped>
.generator {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
    background-color: #f5f5f5;
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
        "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
    background-color: #fff4ec;
}

.generator h1 {
    color: black;
    font-size: 2rem;
    font-weight: 800;
}

.generator .input-content {
    display: flex;
    flex-direction: column;
    width: 27em;
    align-items: center;
    justify-content: center;
}
.generator-input {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    margin: 1rem;
    padding: 1rem 1rem 1rem 1.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
    border-radius: 1.5em;
}

.generator-input .badge {
    font-size: 13px;
    line-height: 13px;
    letter-spacing: 2px;
    padding: 0 1rem;
    text-transform: uppercase;
    font-weight: 800;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    border-radius: 0.5rem;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin: 0 1rem;
    color: white;
    height: 2rem;
}

.weak {
    background-color: #f5203e;
}
.good {
    background-color: #f1c80b;
}

.strong {
    background-color: #43ed9c;
}

.veryStrong {
    background-color: #0070f6;
}

.password {
    width: 100%;
}
.generator-icon {
    min-width: 24px;
    height: 24px;
    margin-left: auto;
    cursor: pointer;
    background: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjUiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNSAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTQuNjMyODEgNC43ODRMNi4xMzI4MSAxMC4wNzE1TTYuMTMyODEgMTAuMDcxNUwxMS41NzAzIDguNzIxNDhNNi4xMzI4MSAxMC4wNzE1QzYuOTA4NjUgNi43NzQxIDkuOTc5NTYgNC41MjE0OCAxMy4zMzI3IDQuNTIxNDhDMTcuNDQyIDQuNTIxNDggMjAuODMyNyA3LjkwODk5IDIwLjgzMjcgMTIuMDIxNUMyMC44MzI3IDE2LjEwNzYgMTcuNDE4OSAxOS41MjE0IDEzLjMzMjcgMTkuNTIxNEM5Ljk0NjggMTkuNTIxNCA2LjgxMjA4IDE3LjE1MzIgNi4wNTc3MyAxMy44MjE0IiBzdHJva2U9IiMwNzFEMkIiIHN0cm9rZS13aWR0aD0iMS4yIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1saW5lam9pbj0icm91bmQiLz4KPC9zdmc+Cg==)
        no-repeat 50%;
}

.length-setting {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 18px;
    font-weight: 800;
    margin: 25px 0;
}

.length-setting label {
    margin-right: 2rem;
}

.btn-circle {
    position: relative;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    padding: 0;
    margin: 0 1.2rem;
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    transition: all 0.1s ease-in;
    background-color: #fff4ec;
}

.btn-circle:hover {
    background-color: #f5f5f5;
}

.length-setting input {
    width: 15rem;
    margin-bottom: 0.7rem;
    height: 4px;
    border-radius: 2px;
    cursor: pointer;
    position: relative;
    z-index: 1;
}

.char-set {
    display: flex;
    align-items: center;
    font-weight: 800;
    font-size: 18px;
}

.char-set .option {
    margin-right: 6rem;
}

.char-set input {
    width: 1.3rem;
    height: 1.3rem;
}

.char-set label {
    margin-right: 1.5rem;
}
</style>
