<h1 align="center"> Weather App Using API </h1>

### We will discuss creating a weather application using tkinter. The GUI app will provide information about temperature, latitude, longitude, date, time, year, country of origin, and other details about the current weather of a particular city.
---

📋 **Modules Request:**
----
---
1. **Tkinter** is the standard GUI library for Python. Python when combined with Tkinter provides a fast and easy way to create GUI applications. Tkinter provides a powerful object-oriented interface to the Tk GUI toolkit.

- Creating a GUI application using Tkinter is an easy task. All you need to do is perform the following steps −

    1. Import the Tkinter module.

    2. Create the GUI application main window.

    3. Add one or more of the above-mentioned widgets to the GUI application.

    4. Enter the main event loop to take action against each event triggered by the user.
    
2. **Requests:** The requests library is the de facto standard for making HTTP requests in Python. It abstracts the complexities of making requests behind a beautiful, simple API so that you can focus on interacting with services and consuming data in your application.    
pip install requests
📋 **Approach:**
---
---
- First, we need to use a weather API (Application Programming Interface) to fetch data from the [Open Weather Map](https://openweathermap.org/) website, and then we need to make a configuration file to store the API key. Finally, we use that configuration file in the Python script.

📋 **Steps to generate an API key:**
----
----
1. Login in the [Open Weather Map](https://openweathermap.org/)
2. Go to the API section. Then in the Current Weather Data section click on the Api doc.
3. Now in the API Call section, we have the link of api.openweathermap.org/data/2.5/weather?q={city name}&appid={API key}
4. Click on the API key on the link it will direct to the page from where you can get the key.

📋 **Steps to create the python3 -- Weather Application using API**
---
----

### 📌 Importing the libraries:


```python
from tkinter import *
import requests
import json
import datetime
from PIL import ImageTk, Image
```

### 📌 Interface of the Application:


```python
root = Tk()
root.title("Weather App")
root.geometry("500x500")
root['background'] = "white"
```

### 📌 Dates:


```python
dt = datetime.datetime.now()
date = Label(root, text=dt.strftime('%A  '), bg='white', font=("Bold", 15))
date.place(x=15, y=130)
month = Label(root, text=dt.strftime('%m %B'), bg='white', font=("Blod", 15))
month.place(x=100, y=130)
```

### 📌 Time:


```python
hour = Label(root, text=dt.strftime('%I : %M %p'),
			bg='white', font=("bold", 15))
hour.place(x=15, y=160)

```

### 📌 Theme for the respective time the application is used:


```python
if int((dt.strftime('%I'))) >= 8 & int((dt.strftime('%I'))) <= 5:
	img = ImageTk.PhotoImage(Image.open('moon.png'))
	panel = Label(root, image=img)
	panel.place(x=210, y=200)
else:
	img = ImageTk.PhotoImage(Image.open('sun.png'))
	panel = Label(root, image=img)
	panel.place(x=210, y=200)

```

### 📌 City Search


```python
city_name = StringVar()
city_entry = Entry(root, textvariable=city_name, width=45)
city_entry.grid(row=1, column=0, ipady=10, stick=W+E+N+S)
```

### 📌 The function where the API calls:


```python
def city_name():

	# API Call
	api_request = requests.get("https://api.openweathermap.org/data/2.5/weather?q="
							+ city_entry.get() + '&APPID=b35975e18dc93725acb092f7272cc6b8&units=metric')

	api = json.loads(api_request.content)

	# Temperatures
	y = api['main']
	current_temprature = y['temp']
	humidity = y['humidity']
	tempmin = y['temp_min']
	tempmax = y['temp_max']

	# Coordinates
	x = api['coord']
	longtitude = x['lon']
	latitude = x['lat']

	# Country
	z = api['sys']
	country = z['country']
	citi = api['name']
```

### 📌 Adding the received info into the screen


```python

	lable_temp.configure(text=current_temprature)
	lable_humidity.configure(text=humidity)
	max_temp.configure(text=tempmax)
	min_temp.configure(text=tempmin)
	lable_lon.configure(text=longtitude)
	lable_lat.configure(text=latitude)
	lable_country.configure(text=country)
	lable_citi.configure(text=citi)
```

### 📌 Search Bar and Button:


```python
city_nameButton = Button(root, text="Search", command=city_name)
city_nameButton.grid(row=1, column=1, padx=5, stick=W+E+N+S)
```

### 📌 Country Names and Coordinates:


```python
lable_citi = Label(root, text="...", width=0,
				bg='white', font=("bold", 15))
lable_citi.place(x=15, y=63)

lable_country = Label(root, text="...", width=0,
					bg='white', font=("bold", 15))
lable_country.place(x=180, y=63)

lable_lon = Label(root, text="...", width=0,
				bg='white', font=("Helvetica", 15))
lable_lon.place(x=15, y=95)
lable_lat = Label(root, text="...", width=0,
				bg='white', font=("Helvetica", 15))
lable_lat.place(x=180, y=95)
```

### 📌 Current Temperature:


```python
lable_temp = Label(root, text="...", width=0, bg = "White",
				font=("Hahmlet",55), fg='black')
lable_temp.place(x=18, y=250)
```

### 📌 Other temperature details:


```python
humi = Label(root, text="Humidity : ", width=0,
			bg='white', font=("bold", 15))
humi.place(x=15, y=400)

lable_humidity = Label(root, text="...", width=0,
					bg='white', font=("bold", 15))
lable_humidity.place(x=107, y=400)


maxi = Label(root, text="Max.Temp. : ", width=0,
			bg='white', font=("bold", 15))
maxi.place(x=15, y=430)

max_temp = Label(root, text="...", width=0,
				bg='white', font=("bold", 15))
max_temp.place(x=128, y=430)


mini = Label(root, text="Min.Temp. : ", width=0,
			bg='white', font=("bold", 15))
mini.place(x=15, y=460)

min_temp = Label(root, text="...", width=0,
				bg='white', font=("bold", 15))
min_temp.place(x=128, y=460)
```

### 📌 The main event loop to take action against each event triggered by the user:


```python
root.mainloop()
```
