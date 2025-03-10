import RPi.GPIO as GPIO
from flask import Flask, render_template, request

app = Flask(_name_)

# Define the GPIO pin for the LED
LED_PIN = 18
GPIO.setmode(GPIO.BCM)
GPIO.setup(LED_PIN, GPIO.OUT)
GPIO.output(LED_PIN, GPIO.LOW)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/light', methods=['POST'])
def light():
    action = request.form.get('action')
    if action == 'ON':
        GPIO.output(LED_PIN, GPIO.HIGH)
    elif action == 'OFF':
        GPIO.output(LED_PIN, GPIO.LOW)
    return ('', 204)

if _name_ == '_main_':
    try:
        app.run(host='0.0.0.0', port=5000, debug=True)
    except KeyboardInterrupt:
        GPIO.cleanup()
