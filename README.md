# Project
import argparse
import requests
import time

# Replace with your WeatherAPI API Key
API_KEY = "fc3db0b9967141a09a5122751230409"
BASE_URL = "https://api.weatherapi.com/v1/"

def get_weather(city):
    # Make a request to the WeatherAPI
    url = f"{BASE_URL}current.json?key={API_KEY}&q={city}"
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        # Extract and display relevant weather information
        print(f"Weather in {city}:")
        print(f"Temperature: {data['current']['temp_c']}°C")
        print(f"Condition: {data['current']['condition']['text']}")
    else:
        print("Error: Unable to fetch weather data.")

def main():
    parser = argparse.ArgumentParser(description="Weather Checking Application")
    parser.add_argument("city", help="City name for weather checking")

    args = parser.parse_args()

    while True:
        get_weather(args.city)
        time.sleep(30)  # Auto refresh every 30 seconds

if __name__ == "__main__":
    main()
