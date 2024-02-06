<template>
	<div class="calculator">
		<div class="display">{{ current || '0'}}</div>
		<div @click="clear" class="btn">AC</div>
		<div @click="sign" class="btn">+/-</div>
		<div @click="percent" class="btn">%</div>
		<div @click="divide" class="btn operator">÷</div>
		<div @click="append('7')" class="btn">7</div>
		<div @click="append('8')" class="btn">8</div>
		<div @click="append('9')" class="btn">9</div>
		<div @click="times" class="btn operator">×</div>
		<div @click="append('4')" class="btn">4</div>
		<div @click="append('5')" class="btn">5</div>
		<div @click="append('6')" class="btn">6</div>
		<div @click="minus" class="btn operator">-</div>
		<div @click="append('1')" class="btn">1</div>
		<div @click="append('2')" class="btn">2</div>
		<div @click="append('3')" class="btn">3</div>
		<div @click="plus" class="btn operator">+</div>
		<div @click="append('0')" class="btn zero">0</div>
		<div @click="dot" class="btn">.</div>
		<div @click="equal" class="btn operator">=</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				previous: null,
				current: '',
				operator: null,
				operatorClicked: false
			}
		},
		methods: {
			clear() {
				this.current = '';
			},
			sign() {
				this.current = this.current[0] === '-' ? this.current.slice(1) : `-${this.current}`;
			},
			percent() {
				this.current = `${parseFloat(this.current) / 100}`;
			},
			clearAfterTotal() {
				if (this.operatorClicked) {
					this.current = '',
					this.operatorClicked = false;
				}
			},
			append(number) {
				this.clearAfterTotal();
				if (this.current.length < 10) {
					this.current = `${this.current}${number}`;
				}
			},
			dot() {
				this.clearAfterTotal();
				if (this.current === '') {
					this.current = '0';
				};
				if (!this.current.includes('.')) {
					this.current = `${this.current}.`;
				} 
			},
			setPrevious() {
				this.previous = this.current;
				this.operatorClicked = true;
			},
			divide() {
				this.operator = (a, b) => {
					if (b == '0') {
						return this.current = 'Ошибка'
					}
					return a / b;
				};
				this.setPrevious();
			},
			times() {
				this.operator = (a, b) => a * b;
				this.setPrevious();
			},
			minus() {
				this.operator = (a, b) => a - b;
				this.setPrevious();
			},
			plus() {
				this.operator = (a, b) => a + b;
				this.setPrevious();
			},
			equal() {
				const total = `${this.operator(
						parseFloat(this.previous),
						parseFloat(this.current) 
					)}`;

				if (total.length < 10) {
					this.current = total;
				} else {
					this.current = total.slice(0, 10);
				}

				this.previous = null;
				this.operatorClicked = true;
				console.log(this.current);
			}
		}
	}
</script>

<style scoped>
	.calculator {
		width: 300px;
		font-size: 40px;
		box-shadow: 0px 0px 16px 4px #878787;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-auto-rows: minmax(70px, auto);
		border: 1px solid #999;
	}
	.display {
		grid-column: 1 / 5;
		padding:30px 15px 10px;
		font-size: 48px;
		text-align: right;
		background-color: #505b7d;
		color: #fff;
	}
	.zero {
		grid-column: 1 / 3;
	}
	.btn {
		padding: 10px;
		background-color: #f2f2f2;
		border: 1px solid #999;
		cursor: pointer;
	}

	.operator {
		background-color: orange;
		color: #fff;
	}
</style>