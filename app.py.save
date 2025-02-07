from flask import Flask, request, jsonify
import math
import requests

app = Flask(__name__)

def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if n % i == 0:
            return False
    return True

def is_armstrong(n):
    digits = [int(d) for d in str(n)]
    power = len(digits)
    return sum(d**power for d in digits) == n

@app.route('/api/classify-number', methods=['GET'])
def classify_number():
    num = request.args.get('number')

    if not num or not num.isdigit():
        return jsonify({"number": num, "error": True}), 400

    num = int(num)
    properties = []
    if num % 2 == 0:
        properties.append("even")
    else:
        properties.append("odd")

    if is_armstrong(num):
        properties.append("armstrong")

    response = requests.get(f"http://numbersapi.com/{num}/math")
    fun_fact = response.text if response.status_code == 200 else "No fun fact available."

    return jsonify({
        "number": num,
        "is_prime": is_prime(num),
        "is_perfect": False,  # You can add logic for perfect numbers
        "properties": properties,
        "digit_sum": sum(int(d) for d in str(num)),
        "fun_fact": fun_fact
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
