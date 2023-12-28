Core ideas :
- Gradual changes is a much safer option than all or nothing.

- Being  able to change without risking breaking unrelated parts is good.

- Small improvements one at the time is safer and adds up to be more than just the sum of them

- Leveraging the power of the masses will get you anywhere.

- We may be working with machines, but we are still working for and along people, efficient communication and sociability aren't buzzwords.

- Knowledge in the information era can be bought at the price of lead and sold at the price of gold. Make " I don't know but I'll find out " your adage.

- "Ain't good carpenter without good tools" get to know your tool and you will increase your productivity by several magnitudes.

- Jack of all Trades, Master of one : have  one or few core technologies, yet dab in many.

- Check assumptions, provide proof for them and write them, unproven assumption is nothing ! 

- The object of your work is to enable others, you're a problem solver

- Take pride in your work, and assume consequences. You're a professional, act like one.

- Don't enable scumbags.

What Makes a pragmatic Programmer ?

In One sentence,
Care about your Craft. Care about programming. Care about Technology.
Why are  you even in the field if you don't ? 

- Early Adopter / fast adapter 
When a new technology comes out,
you should be out there trying it, weighin pros and cons
evaluating the possibilities it offers. Beware of snake oil and miraculous solutions !

- Inquisitive 
You never ask  enough question. Until you know the inside out of something, you should always seek more knowledge. As states the marginal gains philosophy  "By performing many small improvements, you manage to obtain an effect greater than the sum of all small improvements."

- Critical thinker 
Juste because everyone does something in a certain way does not mean there isn't a better way. Remove emotions, keep hard cold facts.

- Realistic 
To hell with unreasonable dead lines and expectations. 
You can be Idealistic in your goals, but when the coding comes,
nothing is worse than over-promising AND under-delivering.
Besides, unrealistic expectations can make you perform worse by 
undermining  your confidence and clouding your judgement.

- Jack of all trades 
Being a specialist whose unable to switch of field is the death of vision, critical thinking and creativity. One should always have many tools in it's toolbox  to be able to tackle any problems. 


### 1. It's Your life
By the time you enter in the workforce, your life condition is your fault.
Programming is among the top fields which provide great control for an individual on it's outcome. Don't like something ? change it or move away from it. "You can change your company or change of  company" _Martin Fowler_ https://wiki.c2.com/?BrainsAsaCheapCommodity

### 2.The cat Ate my source code
A follow up of [[pragmatic-programmer#1. It's Your life]]
but about your code. You are responsible and accountable  for the code (and more broadly, the work ) you output. You consequently should strive to hold it to a high Standard. Which means  
- question (the problem until your intimately familiar with it) 
- prototype (to ensure your answer works) 
- backup (your save files)
- clean (the workspace)
- communicate (your advancement and shortcomings).
When your sentence begins with I don't know ...
make sure it finishes with "but I'll find out ! " / I don't know ___yet___.



### 3.Software Entropy
What happens if you do not respect  [[pragmatic-programmer#2.The cat Ate my source code]] ? Software entropy. Small defects appear, start to accumulate, and before long the whole project is a mess because everyone saw the writings on the wall and stopped trying. 
By all means detect, document and clean software rot before the whole code is lost.  If you find yourself in an already rotting software,
you can start small and accumulate cleaning over the long run. 
As the saying goes "How do you eat an elephant ? One bite at the time."
Also make sure when you are cleaning entropy to not introduce new defects,
otherwise you aren't really cleaning anything.

### 4. Stone Soup 
Three  ideas 
- Teamwork makes the dream work
- Be a catalyst for change / the change you want to see.
- Help yourself and other will come to help you out, maybe eager to join an already rolling train heading straight to success.
It narrates the story of three soldiers coming to a  tight belted belly village after years of wars. No villagers wants to give them food so they sit down 
and decide to boil a stone soup. Before long one villager come and they manage to get him to offer them some herbs for the soup, a small addition.
Then other villager comes and they manage each time to get something a bit more interesting in exchange for sharing a bowl of the upcoming soup. Before long everyone has brought something to the soup, more costly as time passes, and in the end everyone ends up eating a nice soup with many ingredients.

Gradual changes and leveraging  the power of the masses is the key here.

### 5.Good Enough software
Better  is the enemy of Good.
Now don't get me wrong, this isn't a call to mediocrity or to be contempt with crappy barely working software.
This is a call to include the customer in the development so he can make calls on  the trade-off, what functionality is core to his problem, and what is "good enough" for them.


### 6. Your Knowledge Portfolio
Any money invested on knowledge is good money invested period.
If you want to have more granularity, try those tips: 
- Knowledgeable people seek to increase knowledge, see what it means to be a pragmatic programmer.
- Diversify your knowledge and become a Jack of all trades person 
- Diversify also means investing your time in learning not only tried and tested technology, but also dabbing in high risk high reward emerging technologies
- Check periodically for directions to be sure you are learning applicable knowledge

Actions to make you act upon this principle : learn a new programming language, or programming paradigm, or database paradigm, or operating system. Take part in talk sessions, attend or give conferences, take a course, pass a certification.

### 7. Communicate ! 
(efficiently)
- Know what you want to say

- Know the audience
You do not have the same keypoints if you are talking to a customer board,
an engineer board, a marketing board, etc. And if you do, it is time to start thinking in term of their interests ! 
- Choose a style
i.e a style that suits your audience !

- Choose your moment (and format !)
It goes along with Know your audience 

- Polish the presentation 
The best  ideas brought without any care for the form have are on an equal footing with terrible ones nicely packaged.
Even worse if said idea although completely correct is provocative.


- Involve the audience
Your Audience can either be a firing squad, waiting for one wrong step to fall on you  or a thrilled customer, eager to help you sell him something.

- LISTEN TO WHAT THEY SAY FFS
You aren't a dictator are you ? How many stories have you heard where catastrophe could have been avoided if only the main protagonist would have listened to a recurring and objective concern or advice ?

- Get Back to people
Don't be the kind of person who "prouds" himself in being unorganized and forgetting to answer half of their emails. Show dilligency,
and of course, always during work hours only !

A tip for writing documentation.
"Code Never lies, comments sometimes do "
Don't Repeat Yourself
Avoid explaining what is happening, apart from API documentation, their is code for that. Instead explain why something was done this way, 
so if down the line, the code works in a totally different manner,
First the reader will quickly detect it and know to dismiss the old comment,
not be left wondering for hours wether the comment is deprecated or 
Second the reader may be able to trace back why it is no longer done this way.

Generally, each function should be documented as follows  :
What are the valid arguments 
What will be  answered given valid arguments
What it does (read carefully, WHAT it does, not HOW it does, there is code for that !)
Edge case and errors.

### 8. Essence of good design , ETC 
Easy to change. The essence of a good design is allowing ease of modification. Ideologies come and go, methodologies evolve, but all great ones share a common denominator, they promote adaptability. By doing so, they prevent rust, rot and any other pejorative name you can find for  immutable systems.
If you think about it many software development motto promote ETC : 
Separation of Concern, Dependency Inversion, Liskov ,DRY, code factorisation,encapsulation, the Agile Manifesto... .

### 9. DRY and the Devil of duplication
**D**on't **R**epeat **Y**ourself. Have only one source of truth. This applies in Software development, documentation creation, and team management. 
When you have two or more  source of truth, you are guaranteed that one day they will contradict each other. Them all being "source of truth" you'll then have an insurmountable dilemma and will have to repudiate one of them, which will effectively  jeopardize credibility of any work which relied on the repudiated source of truth.

### 10. Orthogonality 
Another name for "maintain  encapsulation" or "separate concern" or " use modularity".
If you modify a portion of code, any unrelated portion should not have to be changed. If by modifying the way a shipping fee is calculated you have to also change  the customer Account display settings, you are in big trouble.
Doesn't Orthogonality principle and DRY contradicts each other ? 
Quit the contrary in fact, if you modify the source of truth, it  literally means you are modifying related components.
If you  are modifying something that is not  the source of truth of a piece of code, then this thing should not change at all, which respects the orthogonality principle.

### 11. Reversibility
This rule is the sum of 
- [[#8. Essence of good design , ETC]] 
- [[#10. Orthogonality]]
You never know when one core dependency will go unmaintained,
one of your core feature no longer supported by a seller, etc. 
By having clean modular design, you can ensure that this does not pose an insurmountable challenge in the future.
Also as stated in the definition of a pragmatic programmer,
beware of fads and passing trends.

### 12.Tracer Bullets 
Key Idea here is to have short iteration cycle with visible results,
to be able to quickly and cheaply get a hold for your idea. 
Attention, this is not about building a prototype that will be scrapped, the moment a proof of concept is made. This is about Checking early, and often that you are developing in the right direction.
Continuous Integration and TDD-based development are big proponents of this idea.

### 13. Prototypes and Post it Notes
A PROTOTYPE IS NOT CODE TO BE USED.
IT IS <u>DISPOSABLE</u> CODE 
A prototype values lies in the lessons learned by producing it.
It can be janky, barely hold together, crash when used in a slightly 
different way than planned that's okay.
The only thing that matters 
Taken precedent paragraph into account, when you prototype here are some tricks you are permitted to use : 
- Wrong data 
- Static Data 
- Incomplete results 
- Ugly UI / terrible UX  ( although particular care should be given to metrics, to learn more lessons )
- placeholder / cookie cutter solutions  to mock up interactions "just to try and see if it works"

### 14. Domain Languages
 The way we speak influence the way we think. 
 Taking this premise, by using well thought names when programming,
 (that is names which relates to the  business domain to which we bring a solution)  
 we allow ourselves  (or even the client when he works with us !) to spot caveats and  nonsense  in the of the software. 
 For example  you work on a Cooking robot,
 by using the words "Stew"  and "clear soup" for example  you can easily spot  nonsense  like if you try to decant a clear soup or to homogenize a stew.
It also ease the communication with the client, removing the need of a translator between what he states and the Architecture of the Software. 

### 15.Estimating
Such a controversial topic, lying clear estimates which are respected throughout. The **Planning fallacy Theory** states that humans are bad ad estimating and if you ask the the time it will take to travel from point A to point B in town by car people will have very similar answer for best case scenario (no traffic jams, only green lights)  and average case scenario. 
Consquently,to enhance the accuracy of your estimates (or lower the consequences if they reveal themselves false by acting in good faith) you can 
- clearly state assumptions necessary to make your estimate , 
		By doing so you can check for errors, and have an explanation to give to an angry customer when things do not go out as planned.
		"
		\ - How many times would it take to download the whole content of this  server ? 
		 \- Assuming there are X Petabytes of data, using a link with a transfer rate 
		of Y Gb/s and  the Hard drive write speed is "Z Gb/s" we can hope that it will take  Result hours. 
		"
- Use the correct time granularity
	Let's say you plan a software development cycle to have a duration of three months. If you express your estimate in terms of days that makes 90 days, an overshoot of 10 days will bring more spotlight than if you laid the estimate in months. It will be no longer "90 days +10 days "
	but "three months plus a bit of overtime"
	
- breakdown your assumption into multiple components
	Just like  ships, by breaking down your assumptions by components, in case of time flood you can mitigate impact and perform a better damage assessment useful for the next time or for planning a new action course.
	
-  Take the time of thinking  
	Giving  an answer out of the blue in a half panicked state rarely comes out accurate, applying all the tips stated asks for calm and  meticulous thinking
	When asked, answer "I'll get back to you in x minutes " and put yourself in the best conditions  to produce the less worst  estimate possible.

- Update your estimate over time 
	Refine them as you go along, it will force you to have difficult conversations but also help other people plan around your shortcomings.

You are a professional, estimate like one. And don't forget if you don't know say "I don't know yet ... but I'll find out !"


### 16. The power or plain text
Fads go, Software goes extinct, business fails, UI is hard to automatize.
What is immune to all of this ? plain text. Save file  Data of a long extinct software can be exploited in plain text.
What is plain text ? Text readable AND understandable by human. Field496=276 is readable yet does not convey much information,Cat_id=276 is immediately understandable.
Plain text does not mean unstructured; JSON,XML and HTTP are all structured yet plain text data formats / protocols.
Moreover, plain text is easily workable with, say hello to all GNU UNIX utilities, text based search, lexical automaton, version control system ... .

### 17.Shell Games
What if we take the power of plain text and apply it to executable ? we get shell. The shell is at the same time 
- A text engine on steroids
- The most powerful interface to communicate with your operating system
	(by powerful we mean modular, and expressive, that is you can do almost everything pertaining to the OS with it.)
Unlike a GUI, you can compose command at will,
you are able make a long list of simple steps" just a few characters away
Unlike a GUI, you are not limited to what you can do, because the limits of the shell are the limits of the system ! (When it is not just a problem of practicity)
Consequently learn your shell

### 18.Power Editing
Just like the shell is the front door on your operating system,
text editing is the front door of your code. Knowing this you should become a power-user when it comes to modifying text with your favorite text editor / IDE. 
You are a power user of your text editor if you cando the following  using ONLY THE KEYBOARD:
- move to , select and move character, word, line, paragraph, syntactic delimiter
- re-indent selection 
- comment selection in one key press 
- Split editor window and navigate between them 
- go to an exact line number, file start, file end 
- search and / or replace by String or regex and repeat this operation on with one keypress
- sort lines 
- recompile / launch 
Learn also how to make macros for your favourite text editor, it will save you on repetitive tasks.
### 19. Version Control 
In the 21st century I doubt any serious business still goes without Version Control on it's code repo. Any here's a list of what it can provide :
- Allow you to see changes applied to code at any point in time, and 
- Allows you and other to collaborate even when offline
-  Allows the automation of testing, code merging, and even delivery to customer
- Force the team to work by increments and to write something to keep track of modifications.
- Helps collaborating when fixing bug or reviewing someone elses code

### 20. Debugging
The action of debugging is often emotionnally charged, it should not.
Tackle the act of debugging as an intricate and interactive puzzle,
or as an act of cleaning like checking for spelling error after you write an email; 
not like a personal attack on your intelligence and your  ability to code.
As such, if you find bug in the code of others do not 
go on high horses, or mock them. Stay factual, fix the issue, explain them
and behave as a professional.
As such here are tips to be efficient.
- Steer clear of emotions
	the moment you start to feel anger or despair, stand up and go for a walk.
	Programming is an intellectual feat that requires all your calm and attention,
	not a half baked and incomplete solution built with anger.

- check assumptions
  	Unless it's an algorithmic problem, bugs are most of the time an the symptom of an incorrect
  	assumption for example :  "I was sure this number would always fit in an short "
  	or "By this point, this object is certainly in X state"
  	maybe " This function call can be performed multiple times in a row without calling an initializer "
   	or even "result cannot be Null"  ?

- find how to reproduce it reliably
  	When you know exactly when a bug is happening, you have done half the work.
  	Indeed you can test later on  if your solution solved the bug, and 

- Read the error message
	You may be rolling your eyes at this point, but I cannot count the number of times I catched someone else
	(or sadly even myself) get an error message, a crash, or a raised exception, who starts to panick and to try
	to fix something right away WITHOUT EVEN READING THE MESSAGE,
	EVEN WITH IT SITTING IN BIG CHARACTERS IN THE FRONT OF THE SCREEN.
	The computer is saying to you what's the problem so no need to take out the ouija board or your crystal ball,
	just listen to what it has to say ! 
- Write down your thought
	The act of debugging can sometimes take the form of a tree: spanning across different branches of varying depth.
	When you have multiple hypothesis, it's best to write them all down so if writing one takes a lot of time / mental
	resources, you still know what were you other hypothesis if it ends up being a dead end.
- Logging will help you immensely
	If only you had a debugger that was constantly running in your production app
	 so you could track everything that happened prior to a crash.
	This thing exists, it is called a logging system. You insert in your code various "notification"
	which will then be saved by the logging system when they are raised, allowing you to see
	what happened at any point in time.
- Rubber ducking, don't bother your colleagues for nothing ! 
	This real practice (see https://en.wikipedia.org/wiki/Rubber_duck_debugging ) allows you to find questions
	to your answer and provide guidance. How come ?
	By narrating step by step the problem you currently have, you'll certainly  fumble a bit  with your explanations on some details.
  	If you fumble it means that you don't understand, if you don't understand, it means there is an unknown which needs to be cleared up.
  	This process using exclusively talking, not listening, it means no need to bother a real human being for this,
  	but because talking all alone can seem a bit strange or unintuitive, you can use a small rubber ducky to act as
  	"an avid listener which never tires, always eager to learn more". 

  - Do not stay stuck 
	If after a certain amount time you still cannot find what the issue is ask for help.
	Do not just say "I'm stuck i don't know why", explain what you have done so far :
	what hypothesis  you have made
	what you have done to test them
	what conclusion you have drawn

	A reasonnable amount of time is an arbitrary amount, but you can take for example 15 minutes.
	When you are stuck spend 15 minutes searching new ideas, checking validity of your hypothesis testing,
	etc. But after 15 minutes have elapsed, if you are still stuck you MUST (not should, MUST) ask for help
	as you otherwise are just wasting your time.

- Use Ockham's razor 
	When facing a bug there are more chances that it comes from your code rather than the legacy very popular library.
  	There is more chance that the error comes from the legacy popular library rather than the OS' kernel .
  	There is more chance that the error comes from the OS' kernel rather than the hardware implementation
  	Not to say that kernel bugs / library bugs /  do not happen, but you'll waste far less time
  	if you start by checking more probable error source rather than a 10 years old piece of code used everyday by millions. 


### 21. Text Manipulation
A Wink to [[# 18.Power Editing]]  and [[#17.Shell Games]]   [[#16.The power of plain text]]
You should know a text manipulation language like sed, awk  or even python / Ruby.
They'll allow you to automate repetitive syntaxic change (like checking for CamelCase for example),
changes that most of the text editor cannot perform. 

### 22. Engineering Daybooks
The authors recommend to work with a small paper notebook with you at all time,
it allows you to keep track informally of thoughts and design decision.
Being informal, it is also easier to drop few words to remember something when you are in a hurry 
rather than opening a rigorous but time consuming planning software.
Of course, don't put passwords or sensitive informations in it !

### 23. Design by Contract
By stating clearly what your function does, you sign a contract.
It is therefore easy to ~~lie blame~~ find the source of problems when things go south. 
A programming contract takes the following form 
- Preconditions  : what inital parameters must be fed / the initial status of the program must be
- Postconditions : what will be returned / what will be the obtained state
- Class invariants Something that is true before the call and after the call (if also in the code we start to dab in algorithmics)
Notice how it resembles very much what you may have been taught in algorithmic class.
- penalties : Fancy word for what will happen if someone does not respect it's part of the contract, exception raised,
  strange inter state mode, etc.

" Be strict about what you accept and greedy about what your return,
if you accept anything, and offer the world in return, you have a lot of code to write !" 





### 24.Dead program tells no lies 
Crash early. 
This may avoid (or at least shorten) the following of a trail of clues to try to find out what caused the problem. 
You also don't have to try to guess what strange state your program is in and how well it can still perform.
Catch and release is for the fish. If you raise an exception while intending to crash early, it is useless
to catch the raised exception just to output a log message, that's what the exception is  for ! 
Morevoer 

### 25. Assertive Programming
Ideally everytime you make an assumption it's because of two things
- the programming languages ensures it for you ( for example in Kotlin variables cannot be null except particular conditions)
- you have code that checks for the assumption 
Assertions fall in the second category.
They are a great runtime way to check assumptions,but they come with limitations.
For example  in Object Oriented Language, child class and functions will not inherit 
your assertions, you'll have to write them again, violating the DRY principle.
Also, in some languages assertions are deactivated by default or 
limited to debugging mode, which slows down code execution.


### 26. How to Balance Resources
multiple tips to manage resources effectively (be it threads, cores, file descriptor, ...)
- Finish what you start (the one reponsible for the allocation of a resource should also be responsible for it's freeing)
- Deallocate from most recent to oldest ( nullyfing the risk of closing a resource still required by something else)
- allocate the same way (If you have multiple resources that are required in the same time when used,
  always allocate them in the same order, prohibiting any dead lock or race condtion ).

### 27. Don't Outrun your headlights
Make small steps and don't make big leap of faith whether it be when planning, refactoring, testing, ...
or you'll find yourself overpromising, and underdelivering.


### 28. Decoupling
You want your code to be flexible and modular, so when the day comes that you have to modify it 
(and trust me it will come !) you are in the best  position to do so. 
Decoupled code is a recurring theme of software development;
in Object Oriented Programming, many features are here to help promote decoupled code :
late dependency linking, abstract class, generalization and specialization, inheritance... .
Functional programming by itself is a promotion of decoupled code : .

As much as Three letters of the five  in the  S.O.L.I.D acronym talk expressly of decoupling 
- the Open-closed principle Open to extension, closed to modification 
- Interface Segregation states that you should have small interfaces so the client depends only
  on what he really needs.
- Dependency Inversion  states that you should depend on abstraction, not implementation

It could even  be argued that the S, Single responsibility principle, stating
that each part of code shall be responsible for one part, and one part only,
is also fighting  coupled code .
  
The symptoms of overly coupled code are very talkative and cannot
be confused with something else : 
- everyone must attend meetings even if they aren't concerned,
  because we don't know what might break next when changing a part of code 
- Changes to one module breaks code in a semantically unrelated place

In the code, tight coupling usually takes the following forms 

Train wrecks : When you have chained method calls that traverse  multiple abstraction layer 
for example let's look at the following 
``` pseudocode
UpdateLateStatus(Customer,12257){
orders = Customer.getorders().getorder(12257)
packages= order.getpackages()
for each package in packages
	if(package.expecteddeliverydate > order.fulldeliverydate ) is True :
		Customer.notifyLate()
		break
}
```
Here we know that there are packages in an order, and many orders in a Customer 
We also know how to check if a package is late package.expecteddeliverydate > order.fulldeliverydate
We shouldn't know any of it, what if tomorrow the way the customer holds olders changes ? 
or the internals of order changes  ? We have to update everything ?! 
"Be strict about what you accept and greedy about what your return" [[# 23. Design by Contract]]
See this corrected version : 
``` pseudocode
UpdateLateStatus(Customer,12257){
order = Customer.getorder(12257)
if order.checkifAnyPackageLate() is true
	Customer.notifyLate()
```
Much better, now we get the order from means that only the customer knows,
and we don't even have to know how are late packages calculated, just call the method !

Globalization :
Global variables are a disaster waiting to happen. Why so ? 
Because they couple distant and unrelated part of the software together. 
By doing so, they introduce software wide states that can change at any moment.
An obvious symptom is when for each test, you have to setup the global variable beforehand.

Putting your global variable inside a Singleton does not change anything. The problem has never been
the number of instances but the very existence of the.

A Global Constant fixed at compilation time is much less problematic,
but beware of it as it can still insert multiple states, which means, more potential bugs.

Inheritance :
Fact : inheritance adds coupling. 
It can be  "good coupling",that is, it is normal or even expected that this code is coupled, by semantic of it.
It can be "bad coupling", usually you used inheritance by laziness or a bad adherence of Don't Repeat Yourself principle.
Always perform Composition unless you have a valid reason of inheriting parent.


### 29. Juggling the real world
The book proposes in this section few methods to make responsive and adaptable program
It could be more or less called 
event driven development.
An event is the information that something is happening 
- the data requested is ready
- the user clicked somewhere
- ...
Four methods are introduced
- Finite State machines
They describe all the possible states and make conditions on what happens
when an event is received in any said state.

They can represent a bit of heavy infrastructure if you have only like two states or be horrendous
if you have 20 states all branching in multiple directions 

- Observer pattern
  Observers make themselves know to the event source that they would like to be notified
  when new events are produced. You can stack many observers with little overhead,
  but it may introduce coupling

- publisher/subscriber
Observer in more generic, coupling is gone but at the price of heavier infrastructure.
Say hello to channels, the bridge between event emitter and receiver
which ensures that one does not have to know the other.

- Reactive programming and Streams
A repetition of publisher ?

### 30. Transforming programming
This part aims to change the way you view programming. It follows a simple yet powerful philosophy :
let the data flow. 
If you see each program like something that justs manipulates then pass it around,
you'll have far less the will to create a "system". Indeed, why build a system with protocol and back checks
and communication protocols when you can just have a one way pipeline ? 
Each time you write code is either
- to create new data
- to modify it
- to pass it around

You may notice how this way of thinking is very close to the paradigm promoted by functional programing,
As little state as possible, function sharing data one after the other ... .

### 31. The inheritance tax 
We come back to inheritance after having opened the case at the end of  part [[# 28. Decoupling]]
Inheritance can be bad because when using it two things are promoted 
everything that the parent contains, the child contains it also the risk here is feature bloat.
Also, since it contains everything from the parent, the child is dependant of everything the parent changes in the future.

If what what was stated above is not a problem for you, or even better is a necessity,
then by all mean go for inheritance. If not, here are three (more two really)  alternatives to inheritance

- Use Standard Protocols to communicate
  This breaks coupling. In Java this means using the "Interface"  keyword.
  You have the opportunity to offer a "à la carte" service where you decide what you offer or not,
  given that your interfaces aren't bloated.

- Delegation
  Basically it's just composition, you contain the object from which you want to share some code or features
  and you pass calls or data whenever needed

- Mixin and traits
A mix of the two above points ,excepted that unlike protocols, here Parent code is at the center of the show
and you add just some functionality by glueing some functions around.


### 32.Configuration
Applications must react to change or be able to be setup by the client.
Consquently they must configurable, the easier, the better.
By providing the ability to configure it  externally, for example through an API or a file, you 
allow yourself and other to automate configuration. What can / will be automated ? 
- the saving 
- the feeding (of a new configuration or the update of it)
- the sharing to other software
The API has the added benefit of not needing to restart the application to load configuration changes.


### 33.Breaking temporal coupling
To perform concurrent programming you need first to understand which steps depends of which.
To Draw an activity diagram first write each atomic step inside a square.
Then for each step  draw arrows, from the step to other for service provided  and from others to the step for dependency.
The steps which do not precedes nor follow each other can be ran in parallel or at least in concurrency (if for example they both exploit a shared ressource ).
Steps which do not have dependency (no arrow pointing towards them) can be ran at any moment when you have 
some downtown.


### 34. Shared state is incorrect state 
Resource management  is more difficult when the software is concurrent because you 
now  have to ensure 
- the resource is shared enough to be used by all who needs it, 
- that two resource requester don't fight for said resource 
To ease this problem we use the motto "Shared state is incorrect state".
It means two agent requiring a shared resource must not make any assumption on it 
until they have ensured that they control it. Otherwise it could lead to a very akward situation
where one agent checks for the availability of a resource, finds out it is free
setups itself for using it, only to found that that in the mean time it had been locked by another agent.



### 35. Actor and processes (Actor and messages would be a more accurate name)
Here is a Work Arrangment that can, without explicit concurrency checking, guarantee safety of execution.
It Bears no shared state, it's the Actor and messages model.
The models consists of two entitites 
- Messages, which can be shared between actors, in one way only (messages are sent from A to B, if B wants to answer to A, it sends a message too)
- Actors who take action when receiving a message 
Actors can be started by other actors or by the program itself. The internal sate of any Actor is unknown to everyone else but itself

Actors could as well be machines, process, processor' core or Thread, the model would work just the same.


### 36. Black Boards
The black board system differs a bit from [[# 35. Actor and processes (Actor and messages would be a more accurate name)]]
Here Actors gather their work from one place and one place only, "a giant black board" which contains all information 
which where deemed shareable at some point by an actor or the problem emitter.
The black board is the only shared resource (or it's content), way easier to monitor for concurrency problems.
This model is particularly useful when the work of some actors could trigger more work that cannot be planned in advance. 
Here we have a "buffet à volonté " where everyone gathers and chooses what suits best his field of expertise to solve.

### 37. Listen to your lizard Brain 
Only interesting bit in this part is the fighting of the blank page syndrome 
1. Write  on a post it "I'm prototyping"
2. Write a comment or two in your empty file describing what you are trying to do 
3. Start typing
4. If you wonder what you are doing right now, look at the post it.
Oh and by the way the "Lizard brain theory" is kind of looked down upon today, see:
https://en.wikipedia.org/wiki/Triune_brain


### 38. Programming by Coincidence 
Programming by coincidence could be defined as 
"not knowing why code works in the first place",
either it be 
- witnessing the program continue to execute "correctly", when an obvious fault is present 
- Using misunderstood (by the programmer) technology, functions, keyword, and glueing them like seen on stack overflow
- more subtle, making assumption based on thin air  before doing something
  "of course the database cursor would be open by this point, there are tons of agent which would use it before me"
- applying patchwork corrections without knowing from where the issue comes in the first place
  "The result is always false, by just 1, so I am going to add 1 to the result every time "
  

It goes without saying that programming by coincidence is bad practice, the correctives for programming by 
coincidence are also simple to ( != easy) 
- If your program continues to execute when you see or have introduced a glaring mistake, something is off.
  Check your assumptions
  (
  	Am i running / compiling the version I am currently editing ? 
  	Is this function really called at this moment ?
  	Is this invariant really respected ?
  ...
  )
  "If your issue is gone without knowing why, you still have  an issue !"
- If you use a technology without understanding what it does, you're just another cargo cult  follower !
  Please, please, please, ***READ THE FUCKING MANUAL*** and never  ever just rely on the name of the function to deduce what it does !
- As always, check your assumptions !
- Error "off by 1"  can  be anything, from a small oversight, to a deep algorithmical error
  "Close enough" is not an acceptable answer ! 



### 39. Algorithm speed
We will here just remind the three algorithmic complexity notations :
let f and g be two function valued in the Real set  
(In algorithmic they usually take a parameter as the size of the problem
and output the time it would take some algorithm to solve it, in arbitrary unit.)
Big O  
f O(g) (f is in big O of g ) if there exist x0 and k both valued in the real set 
so that the following is true 
for any x > x0 
f(x) <= k * g(x)

Omega 
The same as big O except 
that the end result is now 
f(x) >= k * g(x)

 Theta 
f is big Theta G when it its at same time 
Big O of g and Omega of g

Three important notes 
first do not get baited by O
Let's say  f  Theta (log(x)) 
it is AB-SO-LU-TE-LY valid to state that 
f O(x^2), indeed you can take for example k = 10 and x0 = 25 (randomly chosen yet valid numbers)
and check for yourself. Usually though  big O is used by the common programmer as big Theta,
so be extra mindeful when you are talking algorithm complexity

Second, this definitions is true for any given x > x0,
be sure that the common case you code for uses data with a size greater than  x0 ! 
Because usually those great algorithms require a bit of infrastructure which will only slow down the process
for small datasets 

Third point, which echoes with the second,
the most optimum algorithms are usually the hardest to write, debug and maintain,
think about it before using it on a non critical software part,
which Would enhnance the project in no way by being sped up by 80 % 
if it means being an absolute hell of an unmaintainable damage queen.


I recommend this video titled 
"BigO = Performance! And other lies programmers tell themselves!!"
by games with gabe:
https://youtu.be/o4-zpAI7qBc?si=lO8nNKBfQ9PeIZRS

### 40. Refactoring
First a definition,
Refactoring is restructuring / rewriting a body of code,
without changing it's behaviour or results to an outside observer.

Here a few tips to make this essential process painless 
1 Refactoring is NOT for adding functionality, it is for checking on existing and working features
2 We already said it a billion times but, small calculated steps, not big leap of faith
3 A good testing set is almost mandatory for any non trivial refactor, how can reassure yourself  otherwise that the code still behaves as expected ? (Note, tests never have and never will prove that code is valid, only that it doesn't fail yet ! )


### 41. Test to Code
Test as a way to write code : TDD
Test driven development is a way of writing code,
first you write the test, then run it to ensure it fails
then you write the code that makes the code succeed. 
You should end up with working code, and  a test to reassure you when refactoring.

But there is more to that, don't view testing only as a mean or hunting down bug,
which it is not (still waiting for the mathematical proof that enough tests proves that a code is correct).
Instead, view testing as a mean of sharing contract, communicating, and writing good code.
- contract : like the one stated in [[# 23. Design by Contract]]
  They can even be a basis on how to use features of your code, and you can point others to it for examples 
- communicating : code never lies, comments sometimes do,
  by using code to describe other code, we then ensure no lies shall be shared then ! 
- writing good code : Testable code usually mean orthogonal code with clear input and output, just what we want !

Don't get eaten by the test glowfish, 
meaning don't get misguided by the bells and whistle of a test suit passing
TDD is a tool to help you write better code, not to lose yourself in nitty gritty details
and spending hours enlarging your test suite, just because it looks nice 
"Just one more test bro ! "

The best (and hardest) test to write are end to end tests.
As such write your code end to end, it comes with the benefit 
of having something to show to the client, and to avoid once again big leap of faith.
Don't write it from top to bottom, you can't write everything in the specification.
Don't write it from the bottom to the top,  you'll get drown in small details 
without a clear direction

### 42. Property based testing
Writing unit test is tedious. 
Unit tests have a limited scope.
Most of the function we write could be ran a thousand times, without it taking too much time, 
and it would strengthen our confidence in the test suite.
The Answer ? Property based testing  !

It is a type of fuzzing
(see fuzzing https://en.wikipedia.org/wiki/Fuzzing )
(that is, throwing random data to see if program crashes)
Where you specify some interesting ranges of input, and let the software generate them,
and send them to your program to see if it crashes. 
It has the benefit of drastically focusing the test case on interesting points,
which saves time. It is also a drawback, as fuzzing for random input best represents
bug ocurrences and / or a malicious attacker.

### 43. Stay Safe out There
Or How to make your code safe in this dangerous world

- Minimize attack area
Smaller code, smaller API, smaller number of open ports,
smaller tolerance for protocol deviation results in smaller risks.
Exterior  input is a commonly used attack vector, everything coming from  the outside should be treated as
hostile until sanitised. Output data is also a potential attack vector, don't see what I mean ?
"Sorry, your requested password is already used by xxxx" seems a reasonable sentence ?
What do you think about "System crashed, STACK TRACE : ... SSH private key ... "

- Least necessary privilege
If something get's compromised, the less privilege it has, the less it will be able to pivot
and do damage.

- Secure Defaults
  The default settings for your software should be the most secure one, by doing so any oversight
  in settings does not transform into a ticking bomb. Let the (hopefully competent) user
  decide security vs convenience tradeoff.

- Encrypt everything sensitive 
Got a breach and data was stolen ? It will slow the attacker or even fend them off.
Just like least necessary privilege, spend the least amount of time with unencrypted
data in the hands.

- Maintain Security update
You got breached by a software defect patched 9 years ago,
how sad... . Make. Your. Security. Updates.

### 44. Naming Things
A good name convey much meaning in a little character.
For example user vs buyer 
what is user ? a client ? and administrator ? can he do this or this ?
With buyer those questions are answered  in only five letters.
A book (forgot it's title) recommended to have developers and product owners 
share the same industry language , by doing so concepts are  easily conveyed.
When naming, the bigger the scope the bigger the name,
you could get away (please don't) with naming the counter of a one line loop 'i'
but using this same name for a function in a public module should legally allow 
anyone to prosecute you for public insult.


### 45. The Requirement Pit 
We will start this part by a bold stateemnt,
,no one knows exactly what they want.
Given that, we got a bulletproof argument to justify the following
- make small incremental steps and show them to the client to keep in the right direction
  "The job of a programmer is also to help people understand/find out what they want"
  This will avoid you the headache of "It does WHAT I want but NOT HOW I want"
- Things change, current business policy is  NOT the same as hard requirements,
  even requirements may change over time, but business policy should almost be user-configurable.
- Consequently, requirements should be specified as user stories cards explaining the
  situation of the user and his problem we're trying to solve,
  not being  encyclopedia sized hard to read file
- Again, a Glossary built by developer and product owner alike
  helps express tip top requirements and are easier to translate to code.


### 46. Solving impossible puzzles
Not exactly sure why this section lies inside the book, but anyway
When facing a particularly troublesome problem, first determine the limits of the problem
and provide proof for them.  Use those limits to shape how to attack the problem.
And like always don't panic, if you aren't finding an answer caml and focused,
you won't surely find it angry and dissipated.

### 47. Working together
You usually won't work alone on a project, let's make a benefit of it ! 
You can for example pair programming,
one person  with a keyboard, two brains working at the same problem.
It is highly intensive so don't forget to take breaks.
It should result in more maintainable code, with fewer bugs and bad practices,
provided that the one without keyboard isn't slacking off, or that 
if senior and junior developer are put together, ego is kept in check.

Design usually reflect the structure of the  organization  which built it,
you can take advantage of that fact by changing how work is split,
make people work on different modules, rotate them, to ensure all round up code.

Finally, criticize the work, not the person,
you're here to produce great sotfware, not step on people.
Also be open to criticism about your work, or you'll never learn.
Your ego is not your amigo, period.

### 48. The essence of agility
The "agile method" (see https://agilemanifesto.org/)
is over twenty years old now. Widely recognized 
it is ironically sometimes used to promote the exact opposite of it's core ideas.
Stiff, inflexible, unadapted and sluggish  communication,work system and management style.
Here is a reminder of what the manifesto promotes :

- Individuals and interactions OVER processes and tools
- Working software OVER comprehensive documentation
- Custommer collaboration OVER contract negotiation
- Responding to change OVER following plan
  (Or how Helmuth von Moltke the Elder would state "No plan survives first contact with the enemy")


### 49. Pragmatic Teams 
Small teams where trust exists among all of it's members 
will perform better than a bigger team, 
-  communication will flow better (peer to peer communication  link increase is in O(n^2) with n number of members)
- the sense of community will be strong and no one will want to drop the ball on someone else
- it is easier to find out if something is going unnoticed because their are less people to ask if they noticed it
- Just like Fred brooks stated in his book "The mythical man month" stated " If man-hour unit was  valid, 9 women could deliver a baby in a month"


### 50. Coconuts don't cut it 
Do you know why you do everything you do ? 
Why particular framework was chosen, why this tool is used this way,
why this piece of code is included in every file ? 
https://en.wikipedia.org/wiki/Cargo_cult_programming
Remember, your objective is to provide answers to someone problems,
to provide them fast, and they ought to be reliable; not to do like 
everyone else juste because they do it.


### 51. pragmatic Starter Kit
The following are three methods that, once implemented
will free up developer time for more meaningful and money bringing tasks 
- Have your Code in a version control system. Enough Said
- Test early, test relentlessly, automate your testing
  here is a list of different  testing level
  	- Unit testing : the most precise, the most fastidious, yet without them are you really testing ?
  	- Integration testing : Testing brick by brick is good, but do the brick glue together ?
  	- end to end testing : Your user uses a product, not some modules 
  	- performance testing : Because the result is wanted now, not in a week.
  	  Also  thanks to them you can monitor what needs to be optimized.
  	- Saboteur and agent of Chaos : Are you really into testing ? If so make a new branch,
  	  add some bugs and see if they pass through the test suite without triggering an alarm.
  	  You could also simulate failures and see how the software reacts, See https://fr.wikipedia.org/wiki/Chaos_Monkey
	This goes without saying, but saying it is better, if you find a bug, create a test that will catch it
	if it reproduces.
- Automate.
	Manual procedures are a	plague, "oops I forgot this part" or "I swear I did this ... oh well I didn't" or " I invented 		this procedure, I Know it by heart, there is no way I could ... and yet I did."
	Automation provides a guarantee that something WILL be done the same way each time
	Tedious and repetitive tasks which dont require a brain ? automate.


### 52. Delight your user
Software for people other than developers, even more, for everyone except those who develops it,
is a mean to an end. They don't care about technology, they don't care about code structure,
they care that they needs are met. Consequently ask them 
"How will you tell if this project has been successful ?"
You're the enabler, the problem solver.


### 53. Pride and Prejudice
Sign your work. 
"I wrote this code to the best of my ability and I stand behind it."
You're a professional, Act like one.


### 54. Postface : The moral Compass
Don't. Enable. Scumbags.

Developers are gifted people. Programming is one if not the  only 
field when someone can change the world and be a force multiplier, juste by the power of it's intellect.
Have you protected the user, would you use the software yourself ? 
First Do no harm, and don't. enable. scumbags.
