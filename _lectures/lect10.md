---
num: "Lecture 10"
desc: "Linked Lists"
ready: true
lecture_date: 2024-05-07 12:30:00.00-7:00
---

[Recorded Lectures (GauchoCast)](https://gauchocast.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=0a1305b2-d90d-4a41-885a-b14c01652083) 

# Linked Lists

* Python lists are just one way to implement a List type structure
* The underlying structure of a Python List stores information in contiguous memory
	* This is why certain operations like inserting into index 0 requires the shifting of elements to make room
* There is another way to implement a List type structure that performs better in certain operations (and worse in others)
	* This way doesn’t organize data in contiguous memory, so maintaining the list structure doesn’t need to shift elements around
* **Linked Lists** are List collection structures that are not stored in contiguous memory
	* But this structure still provides relative positioning of the data in the List

## Node

* A `Node` is an item in the LinkedList
* A Node contains the data that we are storing in the list and a reference to the next Node in the Linked List

## LinkedList

* A `LinkedList` manages and maintains the chain of nodes as a List collection
* It contains a **head** reference to the **first** node in the Linked List chain
	* As long as we know where the first element is, we can walk down the Linked List and visit every node in the structure
* Methods in the LinkedList class should maintain the links between the nodes
	* These methods maintain the "links" between the nodes in order to keep the LinkedList structure in a valid state

## LinkedList Implementation (Chapter 3.6.2)

```
# LinkedList.py
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

	def getData(self):
		return self.data

	def getNext(self):
		return self.next

	def setData(self, newData):
		self.data = newData

	def setNext(self, newNext):
		self.next = newNext

class LinkedList:
	def __init__(self):
		self.head = None

	def isEmpty(self):
		return self.head == None

	def addToFront(self, item):
		temp = Node(item)
		temp.setNext(self.head)
		self.head = temp

	def length(self):
		temp = self.head
		count = 0
		while temp != None:
			count = count + 1
			temp = temp.getNext()
		return count

	def search(self, item):
		temp = self.head
		found = False
		while temp != None and not found:
			if temp.getData() == item:
				found = True
			else:
				temp = temp.getNext()
		return found

	def remove(self, item):
		current = self.head
		
		if current == None: # empty list, nothing to do
			return

		previous = None
		found = False
		while not found: #Find the element
			if current == None:
				return
			if current.getData() == item:
				found = True
			else:
				previous = current
				current = current.getNext()

		# Case 1: remove 1st element
		if found == True and previous == None:
			self.head = current.getNext()
		
		# Case 2: remove not 1st element
		if found == True and previous != None:
			previous.setNext(current.getNext())
```