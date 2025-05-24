

DongleList Class - Derivative

























# DongleList Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

A list of [dongles](Dongle_Class.html "Dongle Class") connected to the system. The system instance can be found in `licenses.dongles`.

```
dongles = licenses.dongles		# get the DongleList object
print(len(dongles))				# number of Dongles 
print(dongles[0])				# first Dongle in the list
for d in dongles:
	print(d)					# print all Dongles

```

  


## Members

No operator specific members.

  


## Methods

`refreshDongles()`→ `None`:

> Refreshes the list of dongles connected to the system and their product codes.

`encrypt(firmCode, productCode, data)`→ `ByteArray`:

> Encrypts a string or byte array using a CodeMeter dongle with a given firm code and product code installed on it. If successful it returns a byte array with the encrypted data.
> 
> * firmCode - The firm code to use. It must be present on the dongle.
> * productCode - The product code to use. It must be present on the dongle.
> * data - A string or byte array to encrypt. Must be 16 bytes in size at least.

`decrypt(firmCode, productCode, data)`→ `ByteArray`:

> Decrypts a string or byte array using a CodeMeter dongle with a given firm code and product code installed on it. If successful it returns a byte array with the decrypted data.
> 
> * firmCode - The firm code to use. It must be present on the dongle.
> * productCode - The product code to use. It must be present on the dongle.
> * data - A string or byte array to decrypt. Must be 16 bytes in size at least.

`productCodeInstalled()`→ `bool`:

> Returns True if the provided product code is installed on any of the connected dongles.

TouchDesigner Build: 
Latest\n2022.24140
2021.10000
2018.28070
before 2018.28070






Retrieved from "<https://docs.derivative.ca/index.php?title=DongleList_Class&oldid=26976>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")