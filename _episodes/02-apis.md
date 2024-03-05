---
exercises: 20
keypoints:
- You will need to evaluate the suitability of data for inclusion in your corpus and will need to take into consideration issues such as legal/ethical restrictions and data quality among others. 
- Making an API request is a common way to access data. 
- You can build a query using a source's URL and combine it with get() in Python to make a request for data. 
- 
objectives:
- Become familiar with legal and ethical considerations for data collection.
- Practice making an API request to a cultural heritage institution and interpreting responses. 
questions:
- How do I know what data I can use for my corpus? 
- How can I use an API to acquire data?
teaching: 20
title: APIs

---

# Corpus Development- Text Data Collection and APIs

## Sources of text data

The best sources of text datasets will ultimately depend on the goals of your project. Some common sources of text data for text analysis include digitized archival materials, newspapers, books, social media, and research articles. For the most part, the datasets and sources you may come across will not have been arranged with a particular project in mind. The burden is therefore on you, as the researcher, to evaluate whether materials are suitable for your corpus. It can be useful to create a list of criteria for how you will decide what to include in your corpus. You may get the best results by piecing together your corpus from materials from various sources that meet your requirements. This will help you to create an intellectually rigorous corpus that meets your project's needs and makes a unique contribution to your area of study. 

##Text Data and Restrictions

One of the most important criteria for inclusion in your corpus that you should consider is whether or not you have the right to use the data in the way your project requires. When evaluating data sources for your project, you may need to navigate a variety of legal and ethical issues. We’ll briefly mention some of them below, but to learn more about these issues, we recommend the open access book[ Building Legal Literacies for Text and Data Mining](https://berkeley.pressbooks.pub/buildinglltdm/). 


*   **Copyright** - Copyright law in the United States protects original works of authorship and grants the right to reproduce the work, to create derivative works, distribute copies, perform the work publicly, and to share the work publicly. Fair use may create exceptions for some TDM activities, but if you are analyzing copyrighted material, publicly sharing your full text corpus would likely be in violation of copyright. 
*   **Licensing** - Licenses grant permission to use materials in certain ways while usually restricting others. If you are working with databases or other licensed collections of materials, make sure that you understand the license and how it applies to text and data mining. 
*   **Terms of Use** - If you are collecting text data from other sources, such as websites or applications, make sure that you understand any retrictions on how the data can be used. 
*   **Technology Protection Measures** - Some publishers and content hosts protect their copyrighted/licensed materials through encryption. While commercial versions of ebooks, for example, would make for easy content to analyze, circumventing these protections would be illegal in the United States under the Digital Millennium Copyright Act. 
*   **Privacy** - Before sharing a corpus publicly, consider whether doing so would constitute any legal or ethical violations, especially with regards to privacy. Consulting with digital scholarship librarians at your university or professional organizations in your field would be a good place to learn about privacy issues that might arise with the type of data you are working with. 
*   **Research Protections** - Depending on the type of corpus you are creating, you might need to consider human subject research protections such as informed consent. Your institution’s Institutional Review Board may be able to help you navigate emerging issues surrounding text data that is publicly available but could be sensitive, such as social media data. 




##OCR and Speech Transcription

Another criteria you may have to consider is the format that you need your files to be in. It may be that your test documents are not in text format- that is, in a file format that can be copied and pasted into a notepad file. Not all data is of this type, for example, there may be documents that are stored as image files or sound files. Or perhaps your documents are in PDF or DOC files. 

Fortunately, there exist tools to convert file types like these into text. While these tools are beyond the scope of our lesson, they are still worth mentioning. Optical Character Recognition, or OCR, is a field of study that converts images to text. Tools such as Tesseract, Amazon Textract, or Google’s Document AI can perform OCR tasks. Speech transcription will take audio files and convert them to text as well. Google’s Speech-to-Text and Amazon Transcribe are two cloud solutions for speech transcription.

Later in this lesson we will be working with OCR text data that has been generated from images of digitized newspapers. As you will see, the quality of text generated by OCR and speech to text software can vary. In order to include a document with imperfect OCR text, you may decide to do some file clean up or remediation. Or you may decide to only include documents with a certain level of OCR accuracy in your corpus. 


## Using APIs

When searching through sources, you may come across instructions to access the data through an API. An API, or application programming interface, allows computer programs to talk to one another. In the context of the digital humanities, you can use an API to request and receive specific data from corpora created by libraries, museums, or other cultural organizations or data creators. 

There are different types of APIs, but for this lesson, we will be working with a RESTful API, which uses HTTP, or hypertext protocol methods. A RESTful API can be used to post, delete, and get data. You can make a request using a URL, or Uniform Resource Locator, which is sent to a web server using HTTP and returns a response. If you piece together a URL in a certain way, it will give the web server all the info it needs to locate what you are looking for and it will return the correct response. If that sounds familiar, it’s because this is how we access websites everyday! 

###A few things to keep in mind: 

*   Each API will be different, so you will always want to check their documentation. 
*   Some APIs will require that you register to receive an API key in order to access their data. 
*   Just because the data is being made available through an API, doesn’t mean that it can be used in your particular project. Remember to check the terms of use. 
*   Check the data - even if you’ve used the API before. What format will it be delivered in? Is the quality of the data good enough to work with?




## How to Access an API

For an example of how to access data from an API, we will explore [Chronicling America: Historic American Newspapers](https://chroniclingamerica.loc.gov/about/), a resource produced by the National Digital Newspaper Program (NDNP), a partnership between the National Endowment for the Humanities (NEH) and the Library of Congress (LC). Among other things, this resource offers OCR text data for newspaper pages from 1770 to 1963. The majority of the newspapers included in Chronicling America are in the public domain, but there is a disclaimer from the Library of Congress that newspapers in the resource that were published less than 95 years ago should be evaluated for renewed copyright. The API is public and no API key is required. We'll use Chronicling America's API to explore their data and pull in an OCR text file. 

For this lesson, we’ll pretend that we’re at the start of a project and we are interested in looking at how Wisconsin area newspapers described World War I. We aren’t yet sure if we want to focus on any particular newspaper or what methods we want to use. We might want to see what topics were most prominent from year to year. We might want to do a sentiment analysis and see whether positive or negative scores fluctuate over time. The possibilities are endless! But first we want to see what our data looks like. 

By adding search/pages/results/? to our source’s URL https://chroniclingamerica.loc.gov/ and adding some of the search parameters that we have already mentioned we can start building our query. We will want to look for newspapers in Wisconsin between 1914 and 1918 that mention our search term “war.” And to keep our corpus manageable, we want to see only the first pages using sequence=1. If we specify that we want to be able to see it in a JSON file, that will give us the following query: 

https://chroniclingamerica.loc.gov/search/pages/results/?state=Wisconsin&dateFilterType=yearRange&date1=1914&date2=1918&sort=date&andtext=war&sequence=1&format=json

Let’s take a look at what happens when we type that into our web browser. And let’s take a look at what happens when we remove the request to view it in a JSON format. 

Now let's explore making requests and getting data using python. 


```python
!pip install requests
!pip install pandas
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: requests in /usr/local/lib/python3.9/dist-packages (2.27.1)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /usr/local/lib/python3.9/dist-packages (from requests) (1.26.15)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.9/dist-packages (from requests) (2022.12.7)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /usr/local/lib/python3.9/dist-packages (from requests) (2.0.12)
    Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.9/dist-packages (from requests) (3.4)
    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Requirement already satisfied: pandas in /usr/local/lib/python3.9/dist-packages (1.5.3)
    Requirement already satisfied: numpy>=1.20.3 in /usr/local/lib/python3.9/dist-packages (from pandas) (1.22.4)
    Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.9/dist-packages (from pandas) (2022.7.1)
    Requirement already satisfied: python-dateutil>=2.8.1 in /usr/local/lib/python3.9/dist-packages (from pandas) (2.8.2)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.9/dist-packages (from python-dateutil>=2.8.1->pandas) (1.16.0)



```python
import requests
import json
import pandas as pd

from google.colab import drive
drive.mount('/drive')
```

    Mounted at /drive


## Making a request

You can make an API call using a get() request. This will give you a response that you can check by accessing .status_code. There are different codes that you might receive with different meanings. If we send a request that can't be found, we get the familiar 404 code. A 200 response means that the request was successful. 


```python
#What happens when what you are looking for doesn't exist?
response = requests.get("https://chroniclingamerica.loc.gov/this-api-doesnt-exist")
print(response.status_code)
```

    404



```python
#Get json file of your search and check status
#First 20 search results
response20 = requests.get("https://chroniclingamerica.loc.gov/search/pages/results/?state=Wisconsin&dateFilterType=yearRange&date1=1914&date2=1918&sort=date&andtext=war&sequence=1&format=json")
print(response20.status_code)
```

    200


Now that we have successfully used an API to call in some of the data we were looking for, let's take a look at our file. We can see that there are 3,941 total items that meet our criteria and that this response has gotten 20 of them for us. We'll save our results to a text file. 


```python
response20.json() #Converts call to json
data = response20.json() #Turns json into a dictionary
with open('corpusraw.txt', 'w') as corpusraw_file: #Save a copy of the first 20 results
     corpusraw_file.write(json.dumps(data))
```

Next we will look at how we can use the metadata from our results to build a query that use the API to get OCR text from one of the newspaper pages. 

The first four key value pairs in the dictionary object tell us about the results of our query, but the fifth one, with the key 'items' is the one that gives us the bulk of the metadata about the newspapers that meet our requirements. To build our query, we need to grab the id so that we can add it to our URL. We could either manually grab it from our text file or we can call it using its index in the list. 


```python
#Deal with dictionaries within lists
d = data.get('items')
newspaper1 = d[0]
idnewspaper1 = newspaper1.get('id')
print(idnewspaper1)

```

    /lccn/sn85033139/1914-01-01/ed-1/seq-1/


Now that we have the id we need, we can use it to build our query. Adding it to our source's URL gives us https://chroniclingamerica.loc.gov/lccn/sn85033139/1914-01-01/ed-1/seq-1/. To see the OCR for this file, we just need to add ocr.txt to the end of the query to get https://chroniclingamerica.loc.gov/lccn/sn85033139/1914-01-01/ed-1/seq-1/ocr.txt. 

Now let's take a look at what it looks like when we make the request using the API.


```python
#Grab one OCR file from Chronicling America
responsenewspaper1 = requests.get("https://chroniclingamerica.loc.gov/lccn/sn85033139/1914-01-01/ed-1/seq-1/ocr.txt")
print(responsenewspaper1.status_code)
```

    200



```python
print(responsenewspaper1.text)
```

    olume IV.
    tCITY COUHCIL NOUS,
    pecial meeting of the city council
    eld last Saturday evening to take
    i winding up the electric light
    purchase matter and to consider
    otor lire truck purchase matter,
    ler, Gcorgenson and Schroeder
    absent.
    esolutlon of Plumb md Frazier
    unaminously adopted. It ratified
    jKdetail of the committeeâs agree
    â t with the electric company, in
    |Hcted the attorney to apply for a re
    aÃring to enable the stale Railroad
    mjwmission to incorporate the agree-
    Hnt in its order; authorized the coni-
    on electric lights to manage
    H plant temporarily; authorized ihe
    committee to incur some nec
    !iry expenses in priiting and selling
    electric light bonds and instructed
    finance committee not to sell morel
    be bonds than shall be necessary,
    i motion was then made author!/-
    the committee on fire and water to
    to Milwaukee and Kenosha and
    e chief Kratz point out the defects
    advantages of the different types
    notor trucks. Thorison, chairman,
    1 his heart set on this trip. Being
    tious and conscientous above the
    rage he always has to be ââshown.â
    3 vote was, for the junket, 8 against
    The noes were Kapil/, Lippert and
    ierer.
    'he mayor ruled tflat it was an âex
    jrdinary expenditureâ requiring II
    ayes to carry. There was u strained
    pause. Then Thorison came to his
    feet and proposed that the bridge com
    mittee be sent. (This was a short arm
    jab to the solar plexus of his neighbor
    I who recently went on the au
    bridge junket.) Thorison add
    hls committee had numerous
    taake trips of inspection at
    snse of the truck manufactur
    would not consider that and
    the council wanted to spend
    â¢a truck blindly they could not
    snted.
    mtor lire truck proposition for
    ason not discernible has been
    i sinister iniluence for a year
    past. It seems to be creating suspic
    ion and ill-will where there have been
    none for years. Some members are
    fighting it bitterly.
    The necessity for a three-fourths
    vote has prevented the purchase sever
    al times. The proponents caught them
    asleep and slipped the JfiOOO appropria
    tion Into the lodgeu some weeks ago
    specifying it to be for âtire purposes.â
    The antis now assert that this is not
    sufficiently definite to take the purchase
    out of the âextraordinary appropria
    tionâ class. There may be a big light
    over it soon.
    VALUABLE FARM AS
    GIFT STIRSCATO.
    The death of John Meehan of Cato,
    -reported last week, has developed a
    fcurious situation. Mr. Meehan who
    a bachelor, aged 50 has been an
    Hvalid for some time. Early in Nov-
    he gave to the tenant of his
    William Launbrecht, a deed to
    He farm and title to the farm person-
    Hty in consideration of an agreement
    V support the grantor for life and pay
    grantorâs nearest living rela.
    Miss Reddin, of Cato, a niece,
    â BOO upon the grantor's death. The
    farm is just outside the village of Cato.
    Meehan survived this transaction less
    than six weeks. Thus his properly,
    Conservatively valued at SIB,OOO, will
    â  to one not related to him upon the
    â yroent of SIOOO. Meehan had no
    of nearer kin than nieces and
    Although ho had not been
    with these relatives there
    been no ill-will or family feud be
    â¢een them. The farm is further
    pledged upon the bond of Win. Keddin,
    .one of the defendants convicted in the
    treat labor union and; naraile case in the
    federal court at Indianapolis. There
    'are some rumors at Cato of an inten
    tion to contest Launbrecht's possession
    in court but nothing authoritative has
    been made public.
    NOTICE TO TAXPAYERS.
    I Notice is hereby given that the tax
    list'd taxes for the year 11)13 levied
    for the following purposes, ' >wit; Gen
    eral city purposes, state and county
    purposes, schools, sewers, inomelaxes
    special assessments for' sidewalks,
    street improvements and water mains
    and delinquent charges for water
    mains, etc., has been committed to me
    for collection, and that 1 will receive
    kpayment for taxes at my oilice in the
    Hty hall at 931 South Eighth street,
    ni the city of Manitowoc, Wis., for the
    lerm of thirty days next following the
    â ate of this notice.
    I Dated Decern bet 15, 1913.
    I HENRY FRANKE,
    I City Treasurer. Manitowoc, Wis.
    BUY LAND ON EASY TERMS.
    Cut-over hard wood lands In Wiscon
    sin, from $9.00 per acre up. #I.OO per
    here cash, balance in monthly install
    ments of $5 00 on each forty bought.
    No better p/o(>oÃition known. Go to it
    Adv. A. P. Schenian, Agent.
    Subscribe for the Pilot.
    Â®j)c pilol.
    MARRIED
    Miss Serena Westphal and Mr. Her
    man C. Berndt were married at the
    home of the brideâs parents on Christ
    mas day at 5 oâclock in the evening by
    the Rev. of the German
    Lutheran church. The affair was
    quiet, and was witnessed only by the
    immediate relatives of the contract
    ing couple.
    The bride is a bright and accomplish
    ed young lady and has a large circle of
    friends in this city. She is a daughter
    of Mr. and Mrs. H. C. Westphal,
    South 13lh street. She is a graduate
    of the old West Side high school and
    was employed at one time as a deputy
    in the office of the county clerk.
    Mr. Berndt is a well known young
    man, energetic and intelligent, who
    for twelve years was foreman of the
    Pilot, but severed his connection with
    the establishment four months ago to
    accept a more lucrative position with
    the Fond du Lac Reporter. Mr. and
    Mrs. Berndt have taken up their resi
    dence at Pond du Lac.
    The Pilot joins the many friends of
    both bride and groom in tf idering con
    gratulations and expressing the wish
    that their future may be crowned with
    bliss.
    At the home of Win. Ralbsack, Sr.,
    Christmas, Miss Ruth Bern and Mr.
    Melvin Sandersin were united in wed
    lock, the Rev. Haase officiating. Miss
    Adeline Hinz and Arthur Bern, were
    the attendants. The bride is a popular
    young lady who has been employed as
    a clerk in the Esch store. The groom
    is employed as a machinst at the Gun
    nell Machine Company.
    The young couple will make their
    home in this city.
    GOLDEN WEDDING.
    Mr. and Mrs. Christian J. Knutze
    on Tuesday celebrated the fiftieth ar
    niversary of their marriage at theii
    home, North 15th street.
    The marriage of Christian Kuatzen
    and Miss Gunhild Halverson was on
    December ;W, 18113, at Vraadl, Norway,
    the Rev. K. O. Knutzen, father of the
    groom, performing the ceremony.
    Mr. Knutzen is a native of Christi
    ana, Norway, having been born there
    April 1, 1837, being 70 years of age,
    while Mrs. Knutzen, born at Hvidese
    Norway. May 22. 1843, is 70. Despite
    their advanced ages, Mr. and Mrs.
    Knutzen are enjoying good health.
    They came to America the year after
    their marriage, landing at Quebec, and
    later on removing to Chicago. They
    lived in Illinois for a few years and
    came to Manitowoc in 18(37, where they
    have since resided.
    Mr. Knutzen has been a painter con
    tractor for the past 45 years.
    There are five children and fifteen
    grancdhildren living. The children
    are: H. J. Knutzen, Antigo, N. E.
    Knutzen, Green Bay; Mrs. P. A. Holm,
    Tigerton, and Dora and Marie of this
    city.
    There was a family re-union at the
    home Tuesday afternoon and evening.
    The following were here from outside
    for the golden wedding:
    Mrs. Bertha Knutzen, Edwin,George
    Norman, Menasha; Mr,and Mrs. H. J.
    Knutzen, Antigo; Mr. and Mrs. N. K.
    Knutzen, Green Bay; Mr. and Mrs. P.
    A. Holm, Tigerton.
    REAL ESTATE REPORT
    The following Real Estate Reports is
    furnished by the Manitowoc County
    Astract Company, which owns the
    only complete Abstract of Manitowoc
    county.
    George Bauman to Joseph W. Vran
    ey, 108Â£ sq. rods in NW corner sec 30
    Kossuth, SOSOO.
    Annie Derringer et al to Henry
    Baruih, lot 0 blk 312 Manitowoc, $2200.
    John A. Johnson to Arthur E. ILw,
    lot 11 blk 50 Manitowoc, sl.
    John Iâeter Steffes to Peter Endries,
    lots 1 and 2 blk âDâ Manitowoc, *l.
    John Peter StelTes to Peter Endries,
    2J a in sec 23 and 20 Manitowoc Rap
    ids, sl.
    Peter Endries to John Peter StefTes
    et al, lots 1 and 2 blk âDâ Manitowoc
    sl.
    Peter Kndrles to John Peter SteiTes
    24 a in sec 23 2(1 Manitowoc Rapids, sl.
    William Pohl to Norhert Reichert,
    80 a in sec 10 Schleswig, SIO,OOO.
    C. H. Tegen to Mary Healy Jr., lot
    4 blk 291 Manitowoc, fl.
    Matt Kocian to Lawrence Kocian, 120
    a in sec 30 and 31 Cooperstown, sl.
    John G. Meehan to William J. Laun
    brecht, 104.24 a in section 4 Cato and
    36 a in section 33 Franklin, $16,000.
    Charles M. Ohlsen to Jennie M. Ohl
    sen, lot 3 blk 7 Manitowoc, sl.
    Fruit In Glass.
    A housewife who was puzzled to
    know how she could put fruit In the
    refrigerator and not have it scent the
    butter and milk by the side of It,
    caught the Idea of emptying out the
    basket into glass Jars and putting on
    the tops.
    Mental Training.
    An educated man la a man who can
    do what he ought to do when he ought
    to do It whether he wants to do It or
    not.âNicholas Murray Butler.
    DIEO
    Frank Moser dropped dead Monday
    morning on the grounds of the Seventh
    ward public school where he was em
    ployed by contrrctor Steve Knechtel
    in some grading work in progress.
    Mr. Moser had but arrived to begin
    the mornings work and was chatting
    with a fellow employe when he fell
    lifeless without givingany premonitoiy
    symptoms of distress. He had not been
    in ill health. His son Frank died but
    three weeks ago leaving a void in the
    musical circle of the city, he having
    been for years director of the cityâs
    widely known Marine Band. Frank,
    Sr., was born in Hungary in 1854 and
    came to this country in the early 00âs
    and had lived in Maple Grove until 3
    years ago. He was a man of good char
    acter and esteemed by all his neigh
    bors. The Catholic Knights of Wis
    consin, of which he was a member, at
    tended his funeral which was held yes
    terday from St. Bonifact, church to
    Calvary. He is survived only by his
    widow.
    CONNELLY SURPRISED WITH GIFT
    Michael T. Connelly, who is a char
    ter member of the local council of the
    K. of C. organized over 11 years ago,
    and who leaves for Madison today
    to assume anew position with the
    Railroad Commission was entertained
    by his lodge brothers at their hall
    Tuesday evening. Mike was lured to
    the hall by Rev. J. T. O'Leary and un
    suspectingly walked into the party.
    Mikeâs manifold virtues were extolled
    by M. J. OâDonnell, Rev. OâLeary,
    John Egan, P. A. Miller, L. W. Led
    vina, James Taugher, George Kenne
    dy, Dr. A. J, Vits, Puch Egan, Dr.
    Meany and John Carey. Ed. L. Kelley
    gina! verses about the
    ire and Harry Kelley
    marks in presenting a
    uiair on behalf of the
    king that a rocking chair
    was an inspiredly appropriate gift to
    one entering the state service. The
    tenor of most of the tributes was re
    gret at losing the bubbling good spirits
    ofOonneliy. âDynami er of gloom
    Puch Egan called him.
    TRUE SECRET OF POPULARITY
    Qlrl Must. Have torpe Beauty. Grace
    and Intelligence, and Especially
    Radiance.
    What can a young girl, who Is net
    ther a great beauty nor a great heir
    ess, nor one to whom the gods stood
    sponsor at birth, do to make herself
    popular?
    Let us sit down and take our chins
    In our hands and think about It
    A girl must have, at least In some
    small degree, four qualities. There
    are children of fortune who have them
    all, and in abundance, but as from a
    small palette of primary colors a great
    picture may be painted, just so out
    of a few elementary attributes quite
    wonderful results are possible. The
    four qualities of personality are:
    Beauty, grace, intelligence, radk
    ance.
    Beauty may be that of face or fig
    ure, oAAt may be merely an effort of
    beauty through style, charm, or even
    one of the other three qualities fol
    lowing:
    Grace includes not alone symmetrj
    of movement, but all accomplish
    ments In activity, such a a dancing,
    skating, swimming, riding, and also
    any especial gifts, such as a talent for
    music or acting. In other words, the
    girl who has the "gift of graceâ in the
    girl who does things well.
    By intelligence is meant the sympa
    thetic, adaptable quality of mind, rath
    er than that of the brilliant order. Hut
    the one great attribute that crowns
    them all âgranting, of course, some
    gift of the other threeâbut without
    which beauty, grace, cleverness are
    all as applet of Sodomâis the sense
    of enjoyment, the gift of happiness.
    1 dot t think 1 can better define it
    than by tbe word radiance. And best
    of all, radiance is a quality that can
    b( cultivated.
    Beards in Olden Times.
    The Greeks wore their beards until
    the time of Alexander, but that great
    general, probably remembering an en
    counter with bis wife, orderd the Mace
    donians to be shaved, lest their beards
    should g_lve a handle to their enemies.
    Heards were worn by the Romans In
    390 I), C. Th* Emperor Julian wrote
    a diatribe entitled "Misopogonâ against
    the wearing of the chin appendage in
    362 B. C.
    Get Fine Ride.
    All offenders whom It becomes de
    sirable to detain for a greater or less
    period In the new Hordeau Jail, near
    Montreal, are taken to their tempo
    rary dwelling place In a tour'ng car.
    which traverses a beautiful route,
    alongside a river, and with se-ene and
    uplifting scenery In the distance and
    at hand.
    Woman's Reason.
    Women have more of what Is termed
    good sense than men. They cannot
    reason wrong, for tuey do not reason
    at all. They have fewer pretensions,
    are less Implicated In theories, and
    judge of objects more from their im
    mediate and involuntary Impression
    on the mind, and therefore more truly
    and naturally.â Hail'tt.
    MANITOWOC, WIS., THURSDAY, JANUARY I. 1314.
    ITEMS FROM THE PILOT FILES.
    FIFTY YEARS AGO.
    The Fortunes of War.â-A soldier
    of the 17th regulars, a native of Phila
    delphia, at the battle of Chickamauga
    was struck with a piece of shell in the
    right eye, then passing under the
    bridge of the nose destroying the sight
    of the left eye, and he is now perfectly
    blind, though in the prime of life. In
    the same action in which he lost bis
    eyesight, he had a father and three
    brothers killed leaving out of a whole
    family only himself and his aged moth
    er.
    After Them. âGeneral Grant has
    captured, within the past seven months,
    four hundred and twelve cannons,
    namely: fifty-two on his advance to
    Vicksburg, three hundred at that place
    and sixty last week before Chattanoo
    ga. Two thousand United Stales can
    nons were stolen from Norfolk at the
    beginning of the rebellion, but if Grant
    keeps on at this : ate he will soon get
    them all back again. Grant mu it be a
    genuine âson of a gun.â
    Lost Cows Hugh Ray of Kewau
    nee, can find his lost cows at Mr. John
    Sechrest's in the north-west part of
    the town of Two Rivers.
    Meade RetreatsâMore Men!â
    Meade sought Lee. He found him
    When he found him he didnât like his
    looks. So lie ran away. Avery brief
    vis-a-vis with the rebel commander
    scared the wits from our commanderâs
    tiead and gave vigor to his heels.
    Meade thinks Lee too strong for him.
    We think Meade was right. He be
    lieved himself forced to run first, or be
    whipped and then run. Doubtless the
    conclusion was well grounded.
    Now here we are againâflat on our
    backs; without force enough to con
    quer another square rod of southern
    territory. To carry out the plan of
    the government at least a million more
    tpen will be required for the field.
    Under the present draft, we do not gel
    enough to till the places of those who
    die in hospital. If the president is in
    earnest, lie will sweep tlie whole first
    class of enrolled national forces into
    the army at once. At the present rate
    of progress, war is fast getting to be
    chronic.
    Pious That, notoriously pious sheet.
    the N. Y, Independent compv''e,s Presi
    dent Lincoln to a cur with a collar
    Speaking of him, it says: âDoes lie
    not wear Kentucky like a collar to this
    dayV A dog with a collar lights slow!â
    This respectful (V) language is from
    the pen of the Hev. Tilton, editor, who
    was drafted, but, who, though able
    b.idied, concluded not to fight at all.
    TWENTY-FIVE YEARS AGO.
    Charley Peers, Charley Sasse and
    Charley Leveron* constitute a trinity
    of preambulalors on Sundays. A couple
    of weeks ago the three started out in the
    country for a longer walk than usual.
    They took the railroad track until they
    had gone as far as they wished and
    then made for a country mail on which
    they proposed home. â After
    tramping an hour they thought they
    should be in sight of the city but could
    discover no trace of Manitowoc. They
    ipuckened their pace for an other half
    hour and still could discover no trace
    of the lost city. Peers thought some
    one had run away with the pjace; Sas
    se thought there was some witchcraft
    about the thing and Levereniâ. proposed
    they camp out and wait for a relief ex
    pedition. A farmer passed by and the
    three hailed him with. "Say, whereâs
    Manitowocâ?â The farmer thought
    they were guying him and wanted to
    light the crowd. Hasse thought it
    would be a good plan to mount
    and holler as they used to do In olden
    time w hen lost in the woods in hope
    that someone in the city would hear
    and give an answering shout. Their
    queer maneuvers made the farmers
    suspicious and when one of the crowd
    would approach a house to inquire
    about Manitowoc, lie would he chased
    out of the yard with dogs. Peers went
    into the woods having heard at one
    time that persons lost could find ttieir
    way homo by noticing on which side of
    the tree the moss grew. Put it was as
    hard to find moss as it was to lind the
    city. In the meantime the farmers
    were collecting with pitchforks, hoes
    and axes to drive away the three dan
    gerous looking characters who pre
    tended they did not know the way to
    Manitowoc. The trio set olf on a run
    and took anew road. They reached
    the Pranch village by nightfall but
    didnât know the place. One of them
    insisted it was Amigo and that there
    were a few people there who know
    him. Another thought it was Hurley
    as they walked far enough to reach
    that place. The third thought it was
    Depere and pointed to the river as
    proof. They came near having a row
    over the matter but in the nick of
    lime a man approached whom they
    knew. Py round about questions they
    lesrned where they were and hired a
    man to lake them home.
    Now when they go outside the city
    limits for a walk one of âem walks
    backwards so as to keep the city from
    getting awry from them. People who
    meet them wonder why one fellow pre
    fers to walk backward, but the oilier
    i wo explain that he wras born that way.
    They take turns in this task and never
    get beyond sight of the city.
    EDUCATIONAL.
    (ByC. W. Mkisnest.)
    JAN UARY TEACHERSâ M EETINGS
    Usman, Jan. 17, 1914.
    9:30 A. M.
    Opening
    Class Exercise in Middle Form Oleog
    raphy . . Nell to Barnes
    Rural Economics . Edwin Mueller
    Teaching How (o Study (Chapter V)
    Iâ. J. Zimmers
    1;80 P. M.
    How to Teach Long Division, Factoring
    and Decimals - James Murphy
    Ellanora tiraf
    Moral and Humane Teaching
    Marie Gass
    Accident Prevention - Mary (irady
    How to Study (Chapter XI)
    P. J, Zimmers
    Uecdsvllle, Jan. 10, 19H.
    10:00 A. M,
    Singing - - Heedsville Pupils
    Conducted by Gladys VVilllnger
    (a) Accident Prevention
    Mildred Dedricks
    (b) Moral and Humane Teaching
    Etta Hayden
    Teaching How to Study (Chapter V)
    P. J. Zimmers
    1:30 P. M.
    Class Exercise in Agriculture
    Elizabeth Walrath
    Rural Economics - F. O. Christiansen
    How I Teach Factoring, Decimals, and
    Long Division - Florence OâConnors
    P. W. Falvey.
    Teaching How to Study (Chapter XI)
    P. J. Zimmers
    Bring your copy of McMurry lo all
    meetings.
    The state of Maryland is holding sev
    eral educational rallies lo stir up in
    terest in education in order to secure
    legislative action for the improvement
    of the schools of the State and espe
    ciady those located in rural dlstr'cts.
    Rallies are being held in many coun
    ties of the Stale. It is the purpose
    of the State Hoard to hold such rallies
    in every county before the next meet
    ing of the legislature. The State
    Board of Education is especially anxi
    ous to create sentiment which will re
    sult in favorable action Ity the Slate
    legislature on the following mo.-suies;
    1. An increased State appropriation
    for common schools.
    2. A Slate supervisor of rural
    schools ns an assistant to the State Su
    perindent of Public Instruction.
    3. A State-wide compulsory educa
    cation law.
    4. A minimum term of at least sev
    en months for all colored schools.
    . r ). Teacher-training courses in ap
    proved high schools under the auspices
    of the State Board of Education.
    (>. A Slate supported summer school
    for rural teachers.
    It seems strange that so old a state
    as Maryland should lie so far behind
    Wisconsin in these matters; and yet
    the Slate Boaard of Public Affairs bns
    placed Maryland ahead of Wisconsin in
    school efficiency.
    FOLK HIGH SCHOOLS
    IN DENMARK.
    Continuing the education received
    in the elemenlry schools for young
    men and women from 1H to 25 years of
    age and making such provisions as to
    terms that the farm work will boas
    little interfered with as possible is the
    aim of the Folk High Schools of Den
    mark.
    Two courses are offered each year,
    âa four monthsâ course in the winter
    for young men and a three monthsâ
    course in the summer for young wom
    en. Most of these young people have
    completed the work of the elementary
    schools. The schools are located in
    thecountry and are intended primarl'y
    for country youth. The sciences con
    nected with agriculture are taught,
    but the greatest emphasis is laid on
    history, biography, and literature.
    The schools then are not vocational
    schools except in a very broad sense.
    The great object is to awaken the
    intellectual life of the students, lo
    make them ambitious to live efficient
    ly and nobly, and to teach them how
    this may be accomplished.
    It is said that 10 per cent of the pop
    ulation of Denmark goes through these
    schools. Their popularity is attested
    by the fact that they are supported by
    cooperative effort of the people them
    selves; only very small annual grants
    are received from the government.
    â[âhe Folk High Schools are a mighty
    agency :n the life not only of the rural
    communities hut of the nation at large.
    Five members of the Denmark cabinet
    arc from the Folk High Schools, four
    of these are farmers. Many members
    of the lower house of parliament are
    also from these schools. Eighty per
    cent of the officials and managers in
    the cooperative agricultural societies
    and enterprises have attended Folk
    High Schools.
    The results achieved hy these schools
    are a good example of the remarkable
    results which can lie achieved when
    the people are given the kind of educa
    tion which they really need.
    DISEASES OF SCftOOLCHILDREN.
    Tuhercu'osis of the lungs is the lead
    ing cause of deaths among American
    children during the period of school
    life, Next in order ere incidents,
    O.TORRISON COMPANY
    TATE Extend to All Our
    * * Best Wishes for a
    Prosperous and Happy New
    Year and Wish to Thank
    You for the share of patron
    age with which you have
    favored us ...
    We are now in the midst of our
    annual inventory taking and
    beginning with January 2nd you
    will find throughout the entire
    store unusual bargains priced so
    low that if money-saving is the
    object you should look through
    the different departments . .
    O. TORRISON CO.
    First Mortgages and Bonds
    We have on hand and offer for sale choice first mortgages
    and bonds. These mortgages and bonds make the safest
    and best kind examined by ns and we guarantee them
    straight.
    Julius Lindstedt & Cos.
    Manitowoc. WisconsinJ
    dipheria and croup, lyhold fever, and
    organic diseases of the heart. Out of
    a total of 51,1103 deaths from all causes
    at ages 5 to 111,24,510, or 47.5 per cent
    are caused by these live diseases. Tu
    berculosis causes 14,3 per cent and ac
    cidents 13.8 percent of the mortality
    among children of small age. These
    ligures are given In an article in the
    December number of the School Re
    view,
    The light against the great white
    plague should receive renewed im
    petus from the fact that this disease Is
    the captain of the enemies of health
    and life among the school children of
    our land.
    The number of public and private
    high schools in the United Stales of
    fering courses in agriculture is now
    1,880. In 11)10 the corresponding num
    ber was 432, which is about one-fourth
    of the present number.
    Stale Superinlendant C. I*. Cary has
    designated January 28-30 as the days
    for the bolding of the annual conven
    tion of county superimendanls. The
    convention will bo hold in Madison.
    The time and place of meeting will en
    abbâ the county superintendents to lake
    advantage of the meeting of the coun
    try life conference and the two weeks
    Farmers' Course.
    Marriage Licenses
    The following marriage licenses have
    been Issued by the county clerk the
    past week:
    David Terry of Kaukaunn and Nora
    Westpbabl of Two Rivers; Jos. Kolo
    wsky of Milwaukee and Blanche Sol>-
    luosky of Manitowoc; Adolph Ilrat/.
    and Kmrna Hubolz, both of Rockland;
    John liubolz and Laura Rusch, both of
    Rockland; Simon Slsdkey of this city
    and Hernia lieranova of iâraguo, Bo
    hemia; Kdward Shimon and Barbara
    Burish, both of Reedsville; Frank
    Burlsh of Spruce, Wls. and F.mnia Os
    wald of Franklin, Deter Horn and
    Klizabeth Hartman, both of Manitowoc
    Henry Kieselhorst of Newton and Lin
    da Rusch of Liberty; Henry Siege of
    Anti go and Linda Klusmoyor of Ra
    pids; Kdward Kafka and Rose Napic
    clnszkl, both of Two Rivers.
    NUMBER 27
    Joke of Year* Ago.
    A clergyman wan preaching a ser
    mon upon "Death,â in the course ol
    which he asked the question: "Is it
    not a solemn thought?â ills four-year
    old boy, who had been listening in
    rapt attention to his father, Immedi
    ately answered in a shrill, piping
    voice, so as to bo heard throughout
    the house; "Yes, sir, it is."âVintage
    of 1803.
    Peculiar Bequests.
    There is one actual case on record
    of a bequest of artificial teeth. Hut
    as it was so long ago the legal chron
    iclers think the decedent had In mind
    the sale of the teeth to the dentists
    of the time so that cash might be real
    Ued. -Many cases are narrated ol
    women bequeathing their hair to
    their heirs to bo converted Into money.
    Recognized English Holidays.
    There are now twenty six days In
    the year recognized us legitimate oc
    casions for holiday* In most cities of
    Ungland. These are In addition to
    the weekly half-holidays observed on
    Wednesdays or Saturdays. An effort
    Is being made to lessen the number
    of holidays and to bring those re
    tained Into more systematic order.
    Industry Always a Refuge.
    âSome temptations come to the in
    dustrious,â said Spurgeon once, "but
    all temptations come to the Idle " The
    old and good renuly against a be
    setting sin Is to leave neither time
    nor room for It anywhere in life, and
    so crowd it out steadily and surely
    from its old place and power.â
    To Whiten Ivory,
    To whiten Ivory rub it well with un
    salted butter and places it in the sun
    shine. if It Is discolored it may be
    whitened by rubbing it with a paste
    composed of burned pumice stone and
    water and putting in in the sun under
    glass.
    To Clean Brass.
    To clean embossed brass make a
    good lather with soap and a quart ol
    very hot water. Add two teaspoon
    tuls of the strongest liquid ummonla.
    Wash tho article In this, using a soft
    brush for the chased work. Wipe dry
    with a soft cloth.
