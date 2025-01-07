import requests
import json


def get_weather():

    api_key = "MNGWB3X2GMD8TA4CAC63PTFKPj"
    base_url = "http://api.openweathermap.org/data/2.5/weather"

    city_name = input("نام شهر را وارد کنید: ")


    complete_url = f"{base_url}?q={city_name}&appid={api_key}&units=metric&lang=fa"


    response = requests.get(complete_url)

    if response.status_code == 200:
        data = response.json()


        city = data["name"]
        temp = data["main"]["temp"]
        feels_like = data["main"]["feels_like"]
        weather = data["weather"][0]["description"]


        print(f"شهر: {city}")
        print(f"دما: {temp}°C")
        print(f"احساس واقعی: {feels_like}°C")
        print(f"وضعیت هوا: {weather}")
    else:
        print("شهر پیدا نشد یا خطایی رخ داده است.")



get_weather()

