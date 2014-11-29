# dewDrop
## a formal language for social networks


# what

  dewDrop is a simple formal language for use on social networks. 

  Anyone can make statements in dewDrop, and anyone can aggregate those statements to reach conclusions using all the knowledge of their social graph. Only the people you trust - directly or transitively - will have their statements weighted when you build conclusions.

Think wikipedia, with a different official article for each user, depending upon who that user trusts. Anyone can add statements, but how you arrange those statements is up to you.

# why
   
  Online harrassment is a serious problem. Sensitive discussions about important topics are easily derailed by trolls. In addition to runining the experience of a person discussing anything online, trolls can claim to be a member of any group or support any ideology, giving a non-affiliated group a bad name through false flag techniques. 

 With a formal language, we can aggregate statements people make in the language to do things like:

 * Block users who are marked as trolls by a number of my trusted friends
 * When interacting with a stranger, use this person's distance from me on the social graph as a proxy for trustworthiness
 * Incentivize people to admit they have erred - a public record of you apologizing shows you are trustworthy
 * Find out how many self-identified republicans support gay marriage 
 * Find out how many self-identified muslims support ISIS

  Nobody is perfect. This is a known fact. With a public record of the times we have offended people, a person can show that work to obtain forgiveness, and succeed in doing so.  At present, without a formal language or agreed upon record, people have little incentive to apologize when they've offended someone, and no way of knowing if they are dealing with a troll who wants to annoy them, or a caring person who has either misspoken or been misunderstood.

  People who have a record of apologizing when they offend others, and seeking forgiveness for doing so - those are people much more worth talking to. dewDrop can help us find each other.

 # how
  The language can be determined by simple regular expresisons. The primitives are keyworks, hashtags, and urls. A simple parser is implemented in `parser.py`. This is the complete specification for version 1 of the dewDrop language.

## General syntax
  All dewdrop messages can begin with any text; the dewDrop portion starts with #ddv2 to identify it as a dewDrop message. The next token should be a one of the verb keywords of the language. The remaining tokens following the verb should be nouns upon which the verb operates.

    .* #ddv2 <VERB> <NOUN> [<NOUN> ]*

 Most Nouns will be URLS - A user can be referred to with the URL of their social media account. If a dewDrop statement is made on twitter, the '@userName' syntax will be assumed to refer to that person on twitter.  You can also speak about a user account at another site - like a reddit user, a facebook user, an email address, a telephone number... any protocol you wish. 

  The verbs are: "ISA, NOTA, AGREE, DISAGREE, TRUST, DISTRUST, SAMEAS, HURT, SORRY, FORGIVE, THANKS". 
  They are explained below:

## Group Membership
    .* #ddv2 ISA (HASHTAG) [URL [URL]]
    .* #ddv2 NOTA (HASHTAG) [URL [URL]]


Groups in dewdrop are represented by hashtags. A person can claim to be a member of a group with the 'ISA' verb, and claim not to be a meber with the 'NOTA' verb. For example, the sentence

    #ddv2 ISA #democrat

Means "The speaker of this sentence claims to be a member of the #democrat group."  Any group you want to identify with can be used as a hashtag.  This way, discussions around social movements, say "#yesAllWomen", can involve people stating their identification with principles of the group. If I choose to leave a group  - either becuase their values have changed, or I have - I can ussue a 'NOTA' statement:

    #ddv2 NOTA #vegetarian

A person can also make statements about other people.  I can claim that Ralph Nader is a #greeparty member:

    #ddv2 ISA #greeparty @RalphNader


A third argument contains a description. This can be used for evidence of the claim bebeing made, or a vernacular argument.

    
## Statement Agreement
    .* #ddv2 AGREE (URL)
    .* #ddv2 DISAGREE (URL)

  Agreement in dewDrop can be signalled with the AGREE verb.  Disagreement can be signaled with the DISAGREE verb.  A Person can agree with any URL they wish. I might agree with another statement someone has made by agreeing with the url of that statement:

    #ddv2 AGREE https://twitter.com/MarkPNeyer/status/525766862949199873  
 
 I can also agree with a supreme court decision by 'agreeing' with a news article about the supreme court decision, or the wikipedia page. 

  When a discussion evolvs to a certain point, must likely a hashtag will be created to represent the movement. At that point, people who agree with one 'side'  of the discussion will issue a 'group memebership' statement. The point of 'agremeent' statements is primarily to allow people to agree or disagree with other people's statements.

 Suppose Alice, who supports marriage equality, issues a statement:

    @Alice: #ddv2 AMA #LGBTAlly

Now, suppose Bob says:

    @Bob: you said there's no such thing as bisexual #ddv2 NOTA #LGBTAlly @Alice

Bob's statement is equivalent to him saying:

    @Bob: #dd1 DISAGREE https://twitter.com/ALICE/status/1234

Assuming that the url above is the url of Alice's original tweet

  So now suppose more self-identified members of the  group #LGBTAlly weigh in on the discussion. Some may issue AGREE statements with @Alice, and some may issue @AGREE statements with Bob.  A discussion will happen, and either the #LGBTAlly group will  integrate itself, and come to a conclusion, or else it won't and people who can't agree will stop associating under the same banner.

  Suppose that discussion resolves itself, with @Alice agreeing that bisexuality is a natural  thing, too. She may issue statements like this:

    @Alice: you were right about accepting bisexuality #ddv2 SORRY @Bob

Bob may now issue these statements:

    @Bob: it's all good #ddv2 FORGIVE @Alice
    @Bob: #ddv2 AGREE https://twitter.com/Alice/status/1234

As a result of this exchange, the '#LGBTAlly' has increased its integrity; the self-identified members of the group are largely in agreement with each other about what constitutes group membership, AND they have successfully resolved a conflict between two members.  The world is better off! Hooray!

  
## Trust and Distrust
    .* #ddv2 TRUST (URL) [URL [URL]]
    .* #ddv2 DISTRUST (URL) [URL [URL]]

  At lower layer than disagreement is trust. I can disagree with someone, but still believe they are honestly expressing their belief. Users in dewdrop have the ability to state trust and distrust in statements or other users with the 'TRUST/DISTRUST' verbs.
  
  A statement of trust is not a statement of agreement. My mother my say she supports 'traditional marriage' - and although i disagree with her on this, I trust that this is an honest representation of her beliefs.  If someone else comes along and says "I believe all black people are criminals" - I will disagree with this statement. I will only _disrust_ the statement if I have reason to believe that this person is trolling, or does not really believe the thing they are saying.

In a healthy discussion about unpleasant topics, people will disagree. Otherwise there'd be no discussion. It's really not possible to have a healthy discussion with someone you distrust. I suspect dewDrop users will make less frequent use of the 'DISTRUST' verb; it will be used primarily to block trolls. 

If i stay I distrust someone, all of my friends can see that, and may know to stay away from that person and to ignore their messages.

The opposite statement - TRUST - implies that the person i am speaking about is an honest, genuine person. I don't agree with everyone my mom says, but I trust her. I want people who trust me to extend that trust to her - I don't expect them to agree with her, but I would be very surprised if anyone thought she were a troll.

People who are concerned about trolling or being victimized online can follow the TRUST statements issued by their friends to whatever extent they feel comfortable with. Someone who feels comfortable online may say "I'll accept messages from any users whom I can reach through a TRUST-path of length 4 or less."  Someone who feels less comfortable or is more worried about harassment can block or ignore users with a TRUSt-path length of more than 2 - implying they are willing to speak to trusted friends of trusted friends, but not anyone else.

  The 'TRUST' statements allow us to protect each other from trolls.  Anyone is free to disregard these statements, of course - but if I know I can talk to a lot of interesting people following only trusted links from friends, and I know that accepting messages from random strangers puts me at risk of serious harassment - I should have the freedom to choose whom I wish to associate with. 

  I can speak about others' trust or distrust using the three-part syntax. The first URL is the person who is [dis]trustd. The second is the one who does the trust/distrust. The third is a description url; my reasoning for linking the two.

## Same Identity

    .* #ddv2 SAME (URL) (URL)

  This statement may seem small at first, but it actually gives dewDrop a lot of power. It's used to link identities together - so that I can say "this facebook account is the same as this twitter acount", this email address belongs to this account, etc. If @Eve creates a fake account @Fred so she can troll people, and I'm  certain it's @Eve pulling the strings, I can make this statement public: 

    @Bob: #ddv2 SAME @Eve @Fred

People who trust me and are mad at @fred for trolling will not be made at @eve.  The standard mechanism for resoving these disputes applies; people who know @eve may disagree, @fred will probably disagree as well. If there are trusted friends involved that know both of us, they may want to step in to resolve this dispute. If there are no trusted friends, maybe we're all just better off not talking to one another. 


  The 'SAME' statement also allows for a unified sense of personhood to emerge from  multiple social media accounts. I can make a statement about my friend on facebook, and his twitter followers will be able to make sense of the same statement.


## Hurt, Apology, Forgiveness

    .* #ddv2 HURT(URL)[ (URL)[ (URL)]]
    .* #ddv2 FORGIVE (URL)[ (URL)[ (URL)]]
    .* #ddv2 SORRY (URL)[ (URL)[ URL]]

  People upset each other. This happens, and its part of the world. By keeping a record of those we have upset, and those who we've forgiven, we can all help each other get a better gauge of who and how we are. If I run into a stranger on twitter who really upsets me, and I see from his record that a few friends of friends been upset by this guy, but for every single one, he's apologized and they've forgiven him - it suggets that he may be worth talking to. If someone else has offended far fewer people, but has never apologized or been forgiven - it suggests that his offense to me isn't going to change, and I should probably ignore him.

  The syntax for 'hurt' is :
  #ddv2 HURT (person who did the offense) (person who felt offended) (description of the offense)

  
  The syntax for 'forgive' is:
  #ddv2 FORGIVE (person who is being forgiven) (person doing the forgiving) (desciption of the forgiveness)
  
  The syntax for 'sorry' is:

  #ddv2 SORRY (person who is being apologized to) (person who is issuing the apology) (description of the apology)

In all of these, if there is only one argument given, it the value of the second argument corresponds to the person issuing the statement.

  So, If @bob simply wants to say "@Alice has offended me" he can do this

    @Bob: #ddv2 HURT @Alice

  Which is equivalent to this

    @Bob: #ddv2 HURT @Alice @Bob

  Perhaps bob thinks Alice has offended his mother. Then he might say this:

    @Bob #ddv2 HURT @Alice @BobsMama

  If there wre a specific tweet Alice had written, say with address 'http://t.co/123', he might state:

    @Bob #ddv2 HURT @Alice @Bob http://t.co/123


  Maybe alice didn't realize that this was a problem. She might start by immediately apologizing to show good faith:

    @Alice i'm not sure what happened lets talk  #ddv2 SORRY @Bob

  And then she and Bob talk a while, until they found out that Alice made a joke about potato farming, and bob's mother was eaten by a potato. At the end of the conversation, bob says


    @Bob: most people don't know the danger of spuds #ddv2 FORGIVE @alice
    @Bob: i know i overreacted a bit #ddv2 THANKS @alice

 
  And now everyone feels better! Hooray!

  The FORGIVE syntax also allows a person to state their belief that person A has forgiven person B.  The last 'url' field in 'FORGIVE' is a description field. it can be used to explain why the speaker thinks person A forgives person B.


## Thanks

  dewDrop members can say thanks to each other. Isn't that cool? A user who's gotten lots of 'thanks' from friends of friends is probably trustworthy  - but again, that is up to you to decide. The point of dewDrop is merely to give people the ability to speak formally, in a way that there statements can be aggregated into a collective whole. You'll no longer be a drop in the ocean, but an edge in a proof.  Thanks!
  
    .* #ddv2 THANKS (URL)[ (URL)[  (URL)]

  The 'THANKS' syntax follows the same pattern as FORGIVE or HURT. A single url means that the speaker is saying they feel thankful to the identity at that url. Two Urls means the speaker is saying "preson A thanks person B". Three urls mean "person A thanks person B, here are details". 

# warning
  
  I have no idea how this will turn out, but i have some intuition. Suppose you shorted bitcoins in 2010, selling 10,000 bitcoins you didn't for $0.10 apiece. You'd earn yourself a profit of $1,000 - and if you didn't pay them back, you'd be $3,000,000 in debt today. I really think this kind of network could change the world. If you defect against people trying to make the world better, by trolling us - you are standing in the way of human progress. We are building a record book that essentially blocks trolls from the public discourse  - is trolling that group of people really a good idea?

