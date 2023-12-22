Core ideas :
- Gradual changes is a much safer option than all or nothing.

- Being even able to change rules.

- Small improvements one at the time is safer and adds up to be more than just the sum of them

- Leveraging the power of the masses will get you anywhere.

- We may be working with machines, but we are still working for and along people, efficient communication and sociability aren't buzzwords.

- Knowledge in the information era can be bought at the price of lead and sold at the price of gold. Make " I don't know but I'll find out " your adage.

- "Ain't good carpenter without good tools" get to know your tool and you will increase your productivity by several magnitudes.

- Jack of all Trades, Master of one : have  one or few core technologies, yet dab in many.


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

Assertion are a great runtime way to check contract,but they come with limitations.
For example 
Also in Object Oriented Language, child class and functions will not inherit 
your assertions, you'll have to write them again, violating the DRY principle.
unless you are using 
Moreover, in some languages assertions are deactivated by default or 
limited to debugging mode, which slows down code execution.

If you can, crash early. 
This may avoid (or at least shorten) the following of a trail of clues to try to find out what caused the problem 


### 24.Dead program tells no lies 


### 25. Assertive Programming
### 26. How to Balance Resources
### 27. Don't Outrun your headlights
### 28. Decoupling
### 29. Juggling the real world
### 30. Transforming programming

