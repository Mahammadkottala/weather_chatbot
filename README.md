# weather_chatbot
import requests

def get_weather(location):
    api_key = "8c9d36ccb95aff6e0f000cca1aa3bc91"
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": location,
        "appid": api_key,
        "units": "metric"  # Get temperature in Celsius
    }
    response = requests.get(base_url, params=params)
    data = response.json()

    if response.status_code == 200:
        temperature = data["main"]["temp"]
        humidity = data["main"]["humidity"]
        wind_speed = data["wind"]["speed"]
        weather_description = data["weather"][0]["description"]

        return temperature, humidity, wind_speed, weather_description
    else:
        return None

def generate_response(location, temperature, humidity, wind_speed, weather_description):
    if temperature is None:
        return "Sorry, I couldn't retrieve the weather information for that location."

    response = f"The weather in {location} is {weather_description}. "
    response += f"The temperature is {temperature}°C, humidity is {humidity}%, "
    response += f"and wind speed is {wind_speed} m/s."
    return response

def main():
    location = input("Enter a location: ")
    weather_data = get_weather(location)

    temperature, humidity, wind_speed, weather_description = weather_data

    response = generate_response(location, temperature, humidity, wind_speed, weather_description)
    print(response)

if __name__ == "__main__":
  main()
