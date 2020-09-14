import xml.dom.minidom
import time
import os
import string, random
from pathlib import Path
from xml.etree import ElementTree

def customer_id_generator(size=128, chars=string.ascii_uppercase + string.digits):
	return ''.join(random.choice(chars) for _ in range(size))

def random_generator(size=10, chars=string.ascii_uppercase + string.digits):
	return ''.join(random.choice(chars) for _ in range(size))

def main():

	for x in range(0, 5000):

		# new process instance
		Path("./process_instances/%d" % x).mkdir(parents=True, exist_ok=True)

		# use the parse() function to load and parse an XML file
		doc = xml.dom.minidom.parse("offer_00_request.xml");
		
		
		customer_id_generator()
		CustomerID = doc.createElement("CustomerID")
		# CustomerID.setAttribute("Customer", customer_id_generator()  )
		text = doc.createTextNode( customer_id_generator() )
		CustomerID.appendChild(text)
		
		items = doc.getElementsByTagName("Address")
		item = items[0]
		item_chidren = item.childNodes
		item.insertBefore(CustomerID, item_chidren[0])
		
		
		
		# create a new XML file with the results
		#myfile = open("offer_00_request.xml", "w")
		#myfile.write(doc.toprettyxml())
		with open("./process_instances/%d/offer_00_request.xml" % x, "w"  ) as xml_file:
			doc.writexml(xml_file)
		#time.sleep(5)
		
		
		
		
		
		
		
		#############################
		#############################
		#############################
		#############################
		doc = xml.dom.minidom.parse("./process_instances/%d/offer_00_request.xml" % x );
		
		
		
		

		# print out the document node and the name of the first child tag
		print (doc.nodeName)
		print (doc.firstChild.tagName)
		# get a list of XML tags from the document and print each one
		expertise = doc.getElementsByTagName("Address")
		print ("%d expertise:" % expertise.length)
		for skill in expertise:
			print (skill.getAttribute("name"))

		# create a new XML tag and add it into the document
		newexpertise = doc.createElement("Supplierdata")
		newexpertise.setAttribute("Header_image", "data:image/png;base64,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")
		doc.firstChild.appendChild(newexpertise)
		print (" ")
		
		# create a new XML tag and add it into the document
		NearestWarehouse = doc.createElement("NearestWarehouse")
		NearestWarehouse.setAttribute("GeoLocation", "333 Ravenswood Avenue Menlo Park, CA 94025")
		doc.firstChild.appendChild(NearestWarehouse)
		print (" ")

		expertise = doc.getElementsByTagName("Address")
		print ("%d expertise:" % expertise.length)
		for skill in expertise:
			print (skill.getAttribute("name"))

		# create a new XML file with the results
		#myfile = open("offer_01_request_with_address.xml", "w")
		#myfile.write(doc.toprettyxml())
		with open("./process_instances/%d/offer_01_request_with_address.xml" % x, "w"  ) as xml_file:
			doc.writexml(xml_file)
		#time.sleep(5)
		
		
		
		
		
		
		
		#############################
		#############################
		#############################
		#############################
		doc = xml.dom.minidom.parse("./process_instances/%d/offer_01_request_with_address.xml" % x );

		# print out the document node and the name of the first child tag
		print (doc.nodeName)
		print (doc.firstChild.tagName)
		# get a list of XML tags from the document and print each one
		expertise = doc.getElementsByTagName("Address")
		print ("%d expertise:" % expertise.length)
		for skill in expertise:
			print (skill.getAttribute("name"))

		# create a new XML tag and add it into the document
		pricelist = doc.createElement("Prices")
		pricelist.setAttribute("p1", "price 1")
		pricelist.setAttribute("p2", "price 2")
		pricelist.setAttribute("p3", "price 3")
		pricelist.setAttribute("p4", "price 4")
		pricelist.setAttribute("p5", "price 5")
		# doc.firstChild.appendChild(pricelist)
		print (" ")

		expertise = doc.getElementsByTagName("Items")
		print ("%d expertise:" % expertise.length)
		for item in expertise:
			print (item.getAttribute("name"))
			item.appendChild(pricelist)

		# create a new XML file with the results
		#myfile = open("offer_02_request_with_address_and_prices.xml", "w")
		#myfile.write(doc.toprettyxml())
		with open("./process_instances/%d/offer_02_request_with_address_and_prices.xml" % x, "w") as xml_file:
			doc.writexml(xml_file)
		


		#time.sleep(5)
		
		
		#############################
		#############################
		#############################
		#############################
		doc = xml.dom.minidom.parse("./process_instances/%d/offer_02_request_with_address_and_prices.xml" % x);

		# print out the document node and the name of the first child tag
		print (doc.nodeName)
		print (doc.firstChild.tagName)
		# get a list of XML tags from the document and print each one
		expertise = doc.getElementsByTagName("Address")
		print ("%d expertise:" % expertise.length)
		for skill in expertise:
			print (skill.getAttribute("name"))

		# create a new XML tag and add it into the document
		newexpertise = doc.createElement("Comments")
		newexpertise.setAttribute("c1", "asdfl-kaskölfdjhakjsdfhlkasjdfhiuakshdfliuaksjhföoasi4hö89gp4huaöofihe4öohifsaöiyg4uhofesöysgirauörosgihauöshifhaösoyifhoshöeifjesoirjgsoetrgsdrgsdrg")
		newexpertise.setAttribute("c2", "p98segp9749za9gzp4p9zg4aöiuagrklsdrkjgshkurghiöusjekrhögiushrögioslhydrögoisehögiseydorgiseydögsihöeiglsoöeighosheiglhoösitrjgosghtidjgdohöitjiotidthjothidjgoihts")
		newexpertise.setAttribute("c3", "saiofhu9ae4ige48z9t0q3z4gh0a8wotuö4g8hesoa4z8öghsöoeö48hrhusögeos4irsöirhgösoeidrhgsöoeirhgöoseihrgöosueihrgöosuehrgosuerhgöoierhtgoiöehörogihseo5rithgisoerhtgoeir")
		newexpertise.setAttribute("c4", "dgiuhayilsughaiw4g948pa8w4z984gzö98az4wt98qz4piuserzughesrgliuhserögloseöuorildghseiurlsegirishuöesirhösuöhiskjdruszrsieruzsriusjkhrsökhö")
		doc.firstChild.appendChild(newexpertise)
		print (" ")

		expertise = doc.getElementsByTagName("Address")
		print ("%d expertise:" % expertise.length)
		for skill in expertise:
			print (skill.getAttribute("name"))

		# create a new XML file with the results
		#myfile = open("./process_instances/%d/offer_03_request_with_address_and_prices_and_comments.xml" % x, "w")
		#myfile.write(doc.toprettyxml())
		with open("./process_instances/%d/offer_03_request_with_address_and_prices_and_comments.xml" % x, "w") as xml_file:
			doc.writexml(xml_file)
		
		
		
		#y = random_generator()
		#os.rename(r'./process_instances/%d/offer_00_request.xml',r'./process_instances/%d/offer_00_request_{y}.xml' % x )
		
if __name__ == "__main__":
	main();