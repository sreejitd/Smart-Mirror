# Smart-Mirror
Tinkering around a smart mirror interface using Python and a RaspberryPi3B


Things you need:
1. Raspberry Pi 3B
2. A screen
3. A 2-way mirror obviously
4. IR sensor
5.USB Microphone
6. Power input


STEPS:
Step0: import all the required python libraries like locale,threading,requests,json,Tkinter

Step1: Initialize required variables, weather_api ,lattitude,longitude,news_country_code,
	icon_lookup<-array of all the images required


Step2: create class clock
	create time label  
	timeLbl1< - Label(self,..)
	timeLbl1.pack()
	create day  label-  dayOWlbl<- Label(self,..)
	dayOWlbl.pack()
	create date label 
 	datelbl<-Label(self,...)
	datelbl.pack()
	create a  function  tick()  
	update and display time
	timeLbl1.after(200,tick) to call self function every 200 ms to update time etc.


	
Step3: create class weather
	Initialize all the required variables and labels 
	temperature<-'  '
	location<- '  '
	icon<- '  '
	forecast <- '  '
	create a function get_weather
	get_weather():
			weather_req_url<- "darksky.net/forecast..."
			r<-requests.get(weather_req_url) 
			r receives the contents from the website in JSON format
			weather_obj <- json.loads(r.text)
			json.loads decodes the data in Json format to txt format.
			select the icon from the icon{} array based on the weather data 					received from the website
	create a function tick()
	updates the weather
	after(60000,tick) to call tick function every 6000 ms to update time etc.


Step 5:create class NewsHeadline
	pack newspaper image in the Tkinter window	
	image<-Image.open("assets/Newspaper.png")
	photo <-ImageTk.PhotoImage(image)
	iconLbl<-Label(self,image=photo)
	iconLbl.pack()


Step4: create class news
	Initialize required variables
	news_country_code<- '  ' 
headlines_url<- ' "https://news.google.com/news?ned=%s&output=rss"
feedparser is a python module to download and parse feeds
	feed <- feedparser.parse(headlines_url)
	display the first five headlines in the Tkinter window.
	for post in feed.entries[0:5]:
                	headline <- NewsHeadline(self.headlinesContainer, post.title)
                	headline.pack()
 	self.after(600000, self.get_headlines) calls get_headlines function every 600000 ms


Step 5: create class Fullscreen 
	Divide the Tkinter window into Top frame and Bottom Frame
	create object of class news  and use the object to pack the Tkinter window
	news.pack()
	create object of class weather and use the object to pack the Tkinter window
	weather.pack()
	create object of class clock and use the object to pack the TKinter window
	clock.pack()


Step6: Inside main():
	create an object of class Fullscreen as w
	run Tkinter mainloop function with the Fullscreen object.
