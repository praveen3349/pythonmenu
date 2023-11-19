# pythonmenu
print("			Welcome to Menu Project")
print("			.........................")

import subprocess

def open_notepad():
    subprocess.run(["notepad.exe"])

def open_chrome():
    subprocess.run(["chrome.exe"])

def open_whatsapp():
    import pywhatkit
    m=input("pno:")
    h=input("msg:")
    o=input("hr:")
    t=input("min:")
    pywhatkit.sendwhatmsg(m, h, int(o), int(t))

def open_email():
 import smtplib
 import ssl
 from email.message import EmailMessage

 # Define email sender and receiver
 email_sender = 'ppraveen2150@gmail.com'
 email_password = 'xi wxsz wuyc'
 email_receiver = 'ptppraveen2150@gmail.com'

 # Set the subject and body of the email
 subject = 'Check out my new video!'
 body = " hi from linux world "
 
 em = EmailMessage()
 em['From'] = email_sender
 em['To'] = email_receiver
 em['Subject'] = subject
 em.set_content(body)

 # Add SSL (layer of security)
 context = ssl.create_default_context()

 # Log in and send the email
 with smtplib.SMTP_SSL('smtp.gmail.com', 465, context=context) as smtp:
    smtp.login(email_sender, email_password)
    smtp.sendmail(email_sender, email_receiver, em.as_string())
    import imaplib, email

def send_sms():
   import twilio
   from twilio.rest import Client

 # Twilio account credentials
   account_sid = 'AC4caac547521bdf01a9b821a8cd5915b9'
   auth_token = 'f02f2741ff54027502db911648aef102'
   twilio_phone_number = '+18038830970'

 # Create a Twilio client
   client = Client(account_sid, auth_token)
 # Send the SMS
   message = client.messages.create(
    	from_='+18038830970',
 	body =input("typemsg:"),
 	to =input("reciver no:"),
 	)

   print("Message sent successfully")
   print(message.sid)
   
def open_chatgpt():
    # You can customize this based on how you want to interact with ChatGPT
    import webbrowser
    url = 'https://chat.openai.com/auth/login?iss=https%3A%2F%2Fauth0.openai.com%2F' # Replace 'https://www.example.com' with the URL you want to open
    webbrowser.open(url) # Open the URL in the default web browser
    print("Opening ChatGPT...")  
   
def get_geolocation():
    print("Fetching geolocation...")
    # importing geopy library
    from geopy.geocoders import Nominatim
 
 # calling the Nominatim tool
    loc = Nominatim(user_agent="GetLoc")
 
 # entering the location name
    getLoc = loc.geocode("shollinganallur,chennai")
 
 # printing address
    print(getLoc.address)
 
 # printing latitude and longitude
    print("Latitude = ", getLoc.latitude, "\n")
    print("Longitude = ", getLoc.longitude)

def get_twitter_trend():
    print("Fetching current Twitter trends...")
    import webbrowser
    url = 'https://twitter.com/search?q=%23TrendingNow&src=typeahead_click&f=live'
    webbrowser.open(url) # Open the URL in the default web browser
    print("Opening trending topics") 
   
def get_hashtag_posts():
 import requests
 from bs4 import BeautifulSoup
 import webbrowser

 def get_twitter_page_url(topic):
    base_url = "https://twitter.com/search"
    return f"{base_url}{topic.replace(' ', '_')}"

 def open_tiwtter_page(topic):
    url = get_twitter_page_url(topic)
    webbrowser.open(url)

 if __name__ == "__main__":
    topic = input("Enter the # to search on twitter: ")
    open_tiwtter_page(topic)

def get_wikipedia_data():
 import requests
 from bs4 import BeautifulSoup
 import webbrowser

 def get_wikipedia_page_url(topic):
    base_url = "https://en.wikipedia.org/wiki/"
    return f"{base_url}{topic.replace(' ', '_')}"

 def open_wikipedia_page(topic):
    url = get_wikipedia_page_url(topic)
    webbrowser.open(url)

 if __name__ == "__main__":
    topic = input("Enter the topic to search on Wikipedia: ")
    open_wikipedia_page(topic)

def play_audio():
 import pygame

 def play_audio(file_path):
    pygame.mixer.init()
    pygame.mixer.music.load(file_path)
    pygame.mixer.music.play()

 if __name__ == "__main__":
    # Initialize pygame for audio playback
    pygame.init()

    # Get the path to the audio file from the user
    audio_file_path = input("Enter the path to the audio file: ")

    try:
        play_audio(audio_file_path)

        # Keep the program running while the music is playing
        while pygame.mixer.music.get_busy():
            pygame.time.Clock().tick(10)

    except pygame.error as e:
        print(f"Error: {e}")

def play_video():
 import cv2

 def play_video(file_path):
    cap = cv2.VideoCapture(file_path)

    while cap.isOpened():
        ret, frame = cap.read()

        if not ret:
            break

        cv2.imshow('Video Player', frame)

        # Press 'q' to exit the video player
        if cv2.waitKey(30) & 0xFF == ord('q'):
            break

    cap.release()
    cv2.destroyAllWindows()

 if __name__ == "__main__":
    # Get the path to the video file from the user
    video_file_path = input("Enter the path to the video file: ")

    try:
        play_video(video_file_path)
    except Exception as e:
        print(f"Error: {e}")

def adjust_speaker_volume():

 from ctypes import cast, POINTER
 from comtypes import CLSCTX_ALL
 from pycaw.pycaw import AudioUtilities, IAudioEndpointVolume

 def get_volume():
    devices = AudioUtilities.GetSpeakers()
    interface = devices.Activate(
        IAudioEndpointVolume._iid_, CLSCTX_ALL, None)
    volume_interface = cast(interface, POINTER(IAudioEndpointVolume))
    return volume_interface.GetMasterVolumeLevelScalar()

 def set_volume(volume):
    devices = AudioUtilities.GetSpeakers()
    interface = devices.Activate(
        IAudioEndpointVolume._iid_, CLSCTX_ALL, None)
    volume_interface = cast(interface, POINTER(IAudioEndpointVolume))
    volume_interface.SetMasterVolumeLevelScalar(volume, None)

 def change_volume():
    try:
        # Get the desired volume level from the user
        new_volume = float(input("Enter the new volume level (0.0 to 1.0): "))

        # Validate the input range
        if 0.0 <= new_volume <= 1.0:
            set_volume(new_volume)
            print(f"Volume set to {new_volume * 100}%")
        else:
            print("Invalid input. Volume level must be between 0.0 and 1.0.")

    except ValueError:
        print("Invalid input. Please enter a numeric value.")

 def main():
    # Change volume based on user input
    change_volume()

 if __name__ == "__main__":
    main()

# Main menu
while True:
    print("\n==== Menu ====")
    print("1. Notepad")
    print("2. Chrome")
    print("3. WhatsApp")
    print("4. Email")
    print("5. SMS")
    print("6. ChatGPT")
    print("7. Geolocation")
    print("8. Twitter Trend")
    print("9. Hashtag Posts")
    print("10. Wikipedia search")
    print("11. Audio Player")
    print("12. Video Player")
    print("13. Adjust Speaker Volume")
    print("0. Exit")

    choice = input("Enter your choice (0-13): ")

    if choice == "0":
        print("Exiting the program. Goodbye!")
        break
    elif choice == "1":
        open_notepad()
    elif choice == "2":
        open_chrome()
    elif choice == "3":
        open_whatsapp()
    elif choice == "4":
        open_email()
    elif choice == "5":
        send_sms()
    elif choice == "6":
        open_chatgpt()
    elif choice == "7":
        get_geolocation()
    elif choice == "8":
        get_twitter_trend()     
    elif choice == "9":
        get_hashtag_posts()
    elif choice == "10":
        get_wikipedia_data()
    elif choice == "11":
        play_audio()
    elif choice == "12":
        play_video()
    elif choice == "13":
        adjust_speaker_volume()
    else:
        print("Invalid choice. Please enter a number from 0 to 13.")

