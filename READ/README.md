# READ as VRE for the manuscripts written in Newārī and Devanāgarī script

Olga Serbaeva, version 2021.04.02

### Introduction

What is READ? [https://github.com/readsoftware/read](https://github.com/readsoftware/read)
I started to work with READ in December 2020, and here is a sample procedure of what can be done with READ based on the manuscripts of the Jayadrathayāmala. Having selected a single chapter covered by a multiple manuscripts, I would like to guide a potential user through a sample workflow comprising such major items as palaeography, working with the transcript in terms of syntax, lexicography, and dictionaries, text-critical mode, export of the results and further analysis in Python, with dynamic visualisations and publication options.

Here are the steps:

### 0. Preliminary work to be done with the manuscript images
### 1. From adding an item in READ to the palaeographic report
- the logic of item description and structure
- adding images and creating baselines
- adding edition
- basic mark-up of the images 
- linkage and its verification
- working with palaeography table: base-types and defaults
- Palaeography report export
### 2. From diplomatic to text-critical mode of the transcript
- 1. Word list
- 2. Dictionary…
- [to be continued]

### 0. Preliminary work to be done outside of READ with the manuscript images and transcript
#### Images:
Having obtained the manuscript images, it is best if one goes through the whole set of items and checks if there are or not missing folios, wrongly numbered pages, and finds out where are the chapter breaks, images, etc. In a separate document one should present everything which is known about this particular manuscripts and include the information if the images can or cannot be made publicly accessible. I use Protégé for such a DB.
All images are in a single file, and they are numbered as follows:
JY.3_A69r[8/9].JPG
JY.3_A69v.JPG
JY.3_A70r.JPG
JY.3_A70v.JPG
JY.3_A71r.JPG
JY.3_A71v.JPG
JY.3_A72r[9/10].JPG
Here “JY” is a text-abbreviation, “3” is book number, “A” is code for the manuscript that I will use throughout research project, “71r” is a folio-number. In order to find quickly the folios for upload or check up, I also append the chapter splits, i.e. “[8/9]”, meaning that on this folio ends chapter 8 and starts chapter 9.

#### Making preliminary transcript
Besides the folios, we also need to prepare the basic transcript of the manuscript. The closer it is to what is really on the folio, the easier and faster is the work in READ. As I had the full text already transcribed (from the manuscripts A for all 4 books), I only need to modify the transcript to fit exactly any new manuscript.

Sample of JY.3.9_A:
69r3)|| []vaṃ śrutvā devadevī vidyā ghoraparākramā | punaḥ provāca deveśaṃ siṃdhurājārthitā satī || || devy uvāca || śrutaṃ sarvo=
69r4)ttamaṃ sāraṃ rahasyaṃ paramādbhūtam∙ | yaṃ smr̥tvā bhūya evāhaṃ hr̥ṣyāmi ca punaḥ punaḥ | adhunā śrotum icchāmi yā sā pratyaṃmirā parā | sarvasaṅkara=
69r5)doṣaghnī sarvabhāgyāvarohanī | mahāmārī kīrttanāś ca mahāśāntikarī hi yā | sarvayaṃtrogradalanī nāmākhyā hi yathārthataḥ || || bhairava uvāca || 
69r6)śr̥ṇu vakṣyāmi suśroṇi rahasyaṃ pāpanāśanam∙ | pratyaṃgirāvidhiṃ ghoraṃ sarvāriṣṭapramardanam∙ | asyā kālyā sureśāni saptāsaptatikōṭaya=
69r7)ḥ | yaṃtrāṇāṃ dehajāḥ sarvās tenaiṣā maṃtramātrikā | gatvā girivarodyānaṃ guruśiṣyasamanvitaḥ | caṃdanāgurudigdhāṃgo madirānaṃditaḥ || prasta=

#### Conventions for the transcript to be uploaded:
The original transcript encoding should be (state 2021) the UTF8 following the standards of a particular language (here Sanskrit). If some rare letters/symbols are to be used, it has to be modified in the READ DB code, so that the new letters and symbols are listed there, for them to be validated.

Here is the Sanskrit alphabet as it was used throughout this project:
Vowels: a ā i ī u ū ṛ [ṝ] ḷ [ḹ] e ai o au aṃ aḥ
READ uses r̥ and others with a circle below for the semi-vowels, and thus one has to do a bulk replacement of all such letters before uploading
Consonants:
ka (+kṣa) kha ga gha ṅa
ca cha ja jha ña
ṭa ṭha ḍa ḍha ṇa
ta tha da dha na
pa pha ba bha ma
ya ra la va
śa ṣa sa ha
Consonants dis not require any modification. The sorting order for Sanskrit is Sanskrit, “kṣa” is classified under “ka”.
A very important point is virama: “m+virama” = “m∙”, fail to follow this will generate additional syllables in READ.

So far (April 2021) I have used only single and double bars as punctuation signs: | and ||.

There are also the things that are not included so far (April 2021):
Folio numbers
Caesura, or a sign separating 8 and 8 syllables of a pada of a Sanskrit śloka.
Flourishes, i.e. flower-like designs separating the chapters.

The transcript is split in accordance with the physical lines.
The beginning of the line is marked with a folio number followed by the line number with ), i.e. “69r7)”. The ends of the lines do not have any particular mark up unless a. a word is split into 2 lines, in this case it is connected with “=” sign, standing at the end of the first line; and b. when a part of the folio on the right is missing, in this case it is marked as ///. (No occurrence fo far.)

#### Sandhi
One can separate already in the preliminary upload the parts of the composite words with “-” sign, except the places where they overlap on a vowel. There is also a possibility to encode the vowel sandhi of the kind “ā~ā,a a~”, where ā is the vowel where two words overlap, and ~ā,a a~ is its interpretation as ā=a+a. However, these did not work well for my case and I believe that this work is to be done once palaeography is sorted out.I am trying to modify this file 

From adding an item in READ to the palaeographic report

This part of the work is to be done directly in READ.
READ can be installed on a server, and in this case multiple collaborators can access the same instance, or it can be installed locally via Docker. (The technical side of READ, including installation shall be described in a separate document). What follows is described based on my local installation on MAC.

### 1. From adding an item in READ to the palaeographic report

#### 1.0. Landing page of READ

Let us briefly discover the toolboxes and various views of READ.
The view consists of several distinct parts (numbered in red): 
1. Login info: here one can see who has logged in, and the function of the person, i.e. “author”, “editor”, etc.
2. A small part of the database that lists together the projects (ID column) and the titles. This shall be described further in details.
3. The toolbox consisting of multiple small boxes: Find, Edit, View, Layout. 
4. In between Find and Edit is a navigation bar with a “scroll” in red. This button 4 has 2 options: “scroll” and “text”, and in order to add a new document, we shall need the “scroll” one.

<p><img src="https://github.com/DDDOlga/MissingUserManuels/blob/main/READ/IMG1.png" alt="General View of READ after login" width="900"></p>

#### 1.1. The logic of item description and structure
We shall now walk through the creation of a new item in READ. New item means a new project, and the precise organisation of the information is largely up to the researcher. I shall enter all chapters of the JY separately and by manuscripts so that I do not have more than 6-7 manuscript folios per “project”. Depending on the results to be achieved, there is no problems to add even different manuscripts into a single project.

<p><img src="https://github.com/DDDOlga/MissingUserManuels/blob/main/READ/IMG1.png" alt="General View of READ after login" width="900"></p>

#### 1.2. So, how do we create a project in READ?
One should first click on “Find item” (in order to verify if the item exists already or not). Having checked that, on should click on “Add item” in order to create a new one. This opens a rather complex dialogue window, and it is very important to understand the implied structure, as the exports of the results and visualisations shall be based on that.



#### 1.3. Logical structure of an "item" in READ

We see here a hierarchical sequence of quasi independent database entries. Let me explain what this contradictory description means with a graph:

The idea of READ is to classify the project according to items, item being a physical artefact that truly existed in history, i. e. book or scroll, or loose-leaf manuscript. This item can be labeled according to what researcher wants, but one could also use the ID and titles of external databases, for example, NGMPP. Because of personal preferences, I have decided to take each chapter as an “item”.
The item can consist of multiple parts, in my case these shall be the manuscript folios. Read allows the users to assign under the same items the parts that a physically stored in different museums, for example. Each of the parts can have its own IDs and sequences. This is what I mean by “independent database entries.”
Sometimes the parts can be broken into various fragments, meaning physical separation of the pieces, and these again can belong to different collections.
Fortunately, the above being not always the case, and in my project the level of parts if followed by the level of surfaces, which are respectively recto and verso of a folio.
The last level, that of text, serves to link the transcript to the hierarchical structure that includes and explains the images. I.e. I shall be using the same label for the text, because I want to link 1 chapter transcript (JY.3.9_C) to multiple folios on which it physically exists.
One should take care to link all subparts of a given item to a text, i.e. one should repeat the whole hierarchical navigation as many times as one has surfaces in a given item. This is one more reason, why I prefer to work at a chapter, and not at a book level.

While filling in the structure one should press “Enter” after every piece of typed information to be sure that it is saved. READ jumps to sequence 1, part 1 throughout the table, therefore one should scroll down to the desired item every time one needs to expand the information.
The “sequence” in the “part” and the “number” in the “surface” organise the material by order, thus one should enter order numbers there. Result of the last folio of the newly added item will look somewhat like this (fragment left untouched):

Once you click out of the dialogue window, you will see that a blue entry with the label of the item appeared in the toolbox between Find and Edit.

At this point we have finished creating item and can now upload the images. 


#### 1.4. Adding images and creating baselines
We can precisely do this via new grey field which appears down right once the item is created.
In the “Images” line we shall click on “Add new”. A dialogue window opens. 
“Digital” allows to access the online images, for example IIIF. “Private” opens other set of options, in which “User” can be selected as a general recommendation. (Unless the project is truly huge and the collaborators should not access the same images.) One selects and uploads the image, it is confirmed by a pop-up. One should rename the image, if one wishes, for example remove file extension, etc. In order to save the new name, one should click on both “save” buttons, up and down.

Image files should not have empty spaces in the names, these should be replaced by “_”.
The filled in image upload part looks as follows:

One can rename the images by clicking on them even after upload, and also add the tags and annotations.
The first 3 lines of this grey box (I typed there JY.3.9_C), shall be the database entries displayed in the subsection “2” of the landing page of READ (see above). Now, in order to create the base-lines, we should click on the “scroll” button in the tool box. (It might be necessary to do it 2 times or shift-reload READ for the changes to become visible.)
What one sees in the toolbox now, is not only item, i.e. JY.3.9_C, but also a tiny “camera”, and when one clicks on it, the list of uploaded images becomes visible.



Now, in order to create baseline for the palaeography, we should click once on each square sign after +. One will see that the same square sign has appeared in line with “paper” and “camera” signs, and when one clicks on that, one will see the list of created base-lines.

When one clicks now on “Properties” in the “View” subpart of the tool box, one will see that item properties list now not only images, but also base-lines.

#### 1.5. Adding edition
In order to add new edition, i.e. draft manuscript transcript in my case, one should click on the “New edition” in the toolbox.
A dialogue box will open, and there are essentially two options: once one pastes the edition into the window one can validate it line-by-line (select “import as individual freetext lines”) or all at once (“Import lines”). If the 2nd option is selected, the mistakes to be corrected shall appear in the window below. Once all is resolved, the edition can be validated (“Validate multine”). The validation depends on the particular language parameters, but Latin won’t work for Sanskrit, etc.
Having committed multiline one can close the dialogue window.
In READ the data model allows to have more than one edition of a given item.
In order to see the edition, one should in “text mode” (button 4 of the landing page above), drag to the right the blue square into a desires working space.
Now we shall switch to the mark-up of the manuscript images.

#### 1.6. Basic mark-up of the images 
In the “Text” mode as opposed to “Scroll” mode, we shall click on the square meaning “baseline”. Having selected a baseline (any order), we shall drag and drop it to the right. It will open the manuscript folio that is incorporated into HTML.
We shall now mark the syllables/letters on the folio and, at the same time, discover the corresponding part of the toolbox.


#### 1.7. Linkage and its verification ...
#### 1.8. working with palaeography table: base-types and defaults
#### 1.9. Palaeography report export**
