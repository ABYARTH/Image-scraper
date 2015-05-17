# Image-scraper
#This is a web scraper for automatically downloading images to a folder. Created using python, mechanize, Beautifulsoup

import urllib
import mechanize
from bs4 import BeautifulSoup
from urlparse import urlparse
import hashlib

def search(item):           # searching images
	print"finding images"
	img_list = getpicture(item)
	for im in img_list:
		savepicture(im)
		print"done...."

def getpicture(search):      # getting images from web
	browser = mechanize.Browser()
	browser.set_handle_robots(False)
	browser.addheaders = [('User-agent','Mozilla')]
	formatted_images = []
	for z in range(1,8): # i want to search multiple pages of a site, hence the loop
		htmltext = browser.open("page url here"+str(z)+"/") #insert your page url ... notice the concatenation.
		img_urls = []
		soup = BeautifulSoup(htmltext)
		results = soup.findAll("p")
		#print results
		for r in results:
			pics = soup.findAll("img")
			for k in pics:
				if "n.jpg" in k["src"]:
					image_f = k["src"]
					formatted_images.append(image_f)
	#print formatted_images 
	return formatted_images
def savepicture(url):             # for saving images in a folder
	hs = hashlib.sha224(url).hexdigest()
	file_extension = url.split(".")[-1]
	#print url
	folder = "C:/Users/Abyarth/Desktop/web scraping/new folder/pics.jpg"
	#fp = open(uri, 'wb')
	#if url !="":
	urllib.urlretrieve(url, folder)
	destination = folder+hs+"."+file_extension
	#print dest
	urllib.urlretrieve(url, destination)

search('what you want to search')		


# My initial attempt at scraping. This program will be modified and made better with time.
