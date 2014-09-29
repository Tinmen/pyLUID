pyLUID
======

#####A Python Implementation of the LUID (Legible Unique ID) Standard

## Goal

>To provide a framework for globally unique IDs that are easy to use for machines and their human companions.

#### What is a Legible Unique ID?
Legible is defined as easily readable, or capable of being discerned or distinguished. The following is an example LUID.

```
b2b-b-4su53n
```
The above code is seperated into three parts.

Domain | Group  | ID 
------------|------------|----
"b2b"|"b"|"4su53n"

**Domain Code** - This can be any alphanumeric key. It defines the top level of the domain. The rule is that it is any number of characters preceding the first `-`. If someone sees `b2b` someone will know they are looking at an LUID for the company BooksToBrains. It doesn't need to be unique universially but within your system it should be. 

**Group Code** - This can contain any alphanumeric keys and includes `-`. It is used to differenciate between different groups or tables within the project so it must be unique underneath a Domain. The above example is a group code for Books. An example with aditional `-`s is `d-zh-tw` (a dictionary for traditional chinese used in Taiwan). You are only limited by how far you are willing to push the usibility for your users. Additionally you can have no group code so it would look like `b2b-4su53n`. However, there can only be one of these per Domain.

**ID Code** - This only contains alphanumeric characters that are not easily confused with one another. The rule is that it can contain any number of characters following the last `-`, and you are not allowed to repeat a certain number of characters in a row, either half the length of the ID (Length of 4 would mean no more than 2) or less than four (Length of 10 will still limit it to 4 in a row). The reasoning for the rule is, that this being the set that will be the longest and has no definition context, it will be the one that will be most easily entered in wrong.

```
LEGIBAL_CHARS = ['a','b','c','d','e','f','g','h','i','j','k','m','n','o','p','q','r',
	       's','t','u','v','w','x','y','z','2','3','4','5','6','7','8','9']
```

#### Why?
It started because I was creating a group of interelated projects and companies and wanted to keep IDs unique across the system. Yes, IDs are not normally exposed but under some circumstances it may be. I couldn't find a standard way to define IDs that met my needs so I brainstormed a system that would cover almost all use cases and remain unique across the whole set of companies as well as hiding the fact that I had less then 10 users at the time. Nothing to kill the awe of a program then to have someone enter in their ID somewhere or expose it in a URL and you are less than 100 (probably less than every cat videon on youtube). Brainstorming led to the following requirements.


##### Requirements


* Not reveal the order in which objects are made. Especially to early adopters
* Globally unique thoughout an entire ecosystem with potentially many companys and projects
* Easily extendible as the system grows
* Be valid in a URL to allow it to be used as a slug
* Reduce human error by:
  * Not using characters that are easy to mistake for others. (0, 1, l, etc...)
  * Using a defined structure that makes it easy to identify at what ID you are looking 
  * Don't repeat numbers or letters to much or it creates readbility problems (dr33333335g How many 3s is that again?)


##### Tradeoffs
I decide to tradeoff a few things in order to meet these needs.
* Number of Keys
  * Less number of characters possibly means less number of unique ids per string. 
  * **Midigation** <br/> Using letters does increase it significantly from simply numbers which is digits^10 to digits^32
* Harddisk, Time, and Processing
  * Because I have not yet found a way to randomly generate unique keys on the fly (mostly because I am not smart enough I think) you need to pregenerate your LUIDs which takes time and space.
  * **Midigation** <br/> Allowing the system to grow without breaking means you can start with fewer IDs and as your needs grow (and hopefully your resources) you can generate more. Generating LUID keys with 4 digits gives you over 1,000,000 possible sets in a few seconds and in a few megabytes. Most projects will find this suffices for a long time.

* Usibility
  * Having a key that is alphanumeric increases complexity when processing them.
  * **Midigation** <br/>I believe by creating easy to use classes and methods you can reduce this to being neglibible and will actually increase consistancy with how you deal with IDs across your system promoting good code practices.



<hr/>
<sub>Copyright (c) James Hancock 2014</sub>
