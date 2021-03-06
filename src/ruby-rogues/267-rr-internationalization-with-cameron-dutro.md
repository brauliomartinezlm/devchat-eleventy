---
layout: layouts/post.njk
title: >
  267 RR Internationalization with Cameron Dutro
date: 2016-07-06 07:00:42
episode_number: 267
duration: 01:01:38
audio_url: https://media.devchat.tv/ruby-rogues/RR267Internationalization.mp3
podcast: ruby-rogues
tags:
  - ruby_rogues
  - podcast
---

02:39 - Cameron Dutro Introduction

- [Twitter](https://twitter.com/camertron)
- [GitHub](https://github.com/camertron)
- [Lumosity](https://www.lumosity.com)
  02:39 - [Internationalization](https://en.wikipedia.org/wiki/Internationalization) vs [Localization](https://en.wikipedia.org/wiki/Localization)05:28 - How important is internationalization?13:54 - Internationalization and Accessibility
- [The Tragedy of the Commons](https://en.wikipedia.org/wiki/Tragedy_of_the_commons)
  Developer Ignorance/Indifference19:43 - Tools
- [Twitter Translation Center](https://translate.twitter.com/)
- [Rosette](https://rosette-proj.github.io)
- [txgh](https://github.com/lumoslabs/txgh)
- [Transifex](https://www.transifex.com)
  24:48 - How can small companies internationalize?26:22 - Crowdsourcing
- [Contributor Covenant](https://contributor-covenant.org/)
  30:34 - People Have Names
- [Patrick McKenzie: Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)
- [Falsehoods Programmers Believe About Phone Numbers](https://github.com/googlei18n/libphonenumber/blob/master/FALSEHOODS.md)
- [Carina C. Zona: Schemas for the Real World @ RubyConf AU 2013](https://www.slideshare.net/cczona/schemas-for-the-real-world-rubyconf-au-201302)
  34:54 - Gender
- I18n, l10n, m10n: Abbreviations for Internationalization, Localization, and Minimization
  39:35 - Educational Resources
- [Rails Guides on Internationalization](https://guides.rubyonrails.org/i18n.html)
- [ICU - International Components for Unicode](https://site.icu-project.org/)
- [twitter-cldr-rb](https://github.com/twitter/twitter-cldr-rb)
- [CLDR - Unicode Common Locale Data Repository](https://cldr.unicode.org/)
  47:14 - [Unicode](https://unicode.org/)
- [Unicode Consortium](https://unicode.org/consortium/consort.html)
- [Aditya Mukerjee: I Can Text You A Pile of Poo, But I Can’t Write My Name](https://modelviewculture.com/pieces/i-can-text-you-a-pile-of-poo-but-i-cant-write-my-name)
  &nbsp; Picks
- [I17n.rb](https://github.com/dbrady/scrapbin/blob/master/stupid/i17n.rb) - Intranumeralization (David)
- [Patrick McKenzie: Falsehoods Programmers Believe About Names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/) (David)
- [Mogo Portable Active Office Chair](https://store.focalupright.com/mogo-seat-p/fks-1000.htm) (Sam)
- [Richard Schneems: Saving Sprockets](https://schneems.com/2016/05/31/saving-sprockets.html) (Coraline)
- [Calvino Noir](https://mcro.org) (Coraline)
- [ICU](https://site.icu-project.org/)(Cameron)
- [CLDR](https://cldr.unicode.org/) (Cameron)
- [twitter-cldr-rb](https://github.com/twitter/twitter-cldr-rb) (Cameron)
- [Hacknet](https://store.steampowered.com/app/365450/) (Cameron)
- [Golden State Warriors](https://www.nba.com/warriors/) (Cameron)

### Transcript

**SAM:&nbsp;** So can someone please tell me why we're discussing a topic that is eight syllables long? Do we hate ourselves that much?

**_[This episode is sponsored by Hired.com. Every week on hired they run an auction where over a thousand tech companies in San Francisco, New York, and L.A. bid on Ruby developers providing them with salary and equity upfront. The average Ruby developer gets an average of 5 to 15 introductory offers and an average salary offer of $130,000 a year. Users can either accept an offer and go right into interviewing with a company or deny them without any continuing obligations. It’s totally free for users. And when you’re hired, they give you a $1,000 bonus as a thank you for using them. But if you use the Ruby Rogues link, you’ll get a $2,000 instead. Finally, if you’re not looking for a job but know someone who is, you can refer them to Hired and get a $1,337 bonus if they accept the job. Go sign up at Hired.com/RubyRogues.]_**

**_[I’m excited to tell you about a new sponsor to the show, Rollbar. One of the frustrating things about being a developer is dealing with errors. Ugh. Relying on users to report errors, digging through log files to debug issues, or a million alerts flooding your inbox ruining your day. With Rollbar’s full-stack error monitoring, you get the context and insights and control you need to find and fix bugs faster. It’s easy to install. You could start tracking production errors and deployments in eight minutes or less, or automatically create new issues in GitHub, JIRA, Pivotal Tracker, et cetera. They have a special offer for Ruby Rogues listeners. Go to Rollbar.com/RubyRogues to sign up and get the bootstrap plan free for 90 days. That’s 300,000 errors tracked free. Give Rollbar a try today. Go to Rollbar.com/RubyRogues.]_**

**_[This episode is sponsored by Shippo. Shippo is a shipping API that connects you with over 15 different shipping carriers such as FedEx, UPS, USPS, Canada Post, and UberRUSH in one integration. You can use Shippo’s APIs to compare shipping rates across carriers, print discounted labels, validate shipping addresses, track packages, and power your shipping in many different ways. You can connect directly to the API or use the provided Shippo Ruby gem to print your first label in a few minutes. The Shippo API is free to use. You only pay for the actual shipping label and a five-cent label fee. Sign up by going to GoShippo, that’s G-O-S-H-I-P-P-O dot com slash Ruby Rogue to get six months with zero label fees.]_**

**CORALINE:&nbsp;** Hello and welcome to Ruby Rogues. Today in our panel, we have David Brady.

**DAVID:&nbsp;** Sky TV listeners, press the red button now.

**CORALINE:&nbsp;** Sam Livingston-Gray.

**SAM:&nbsp;** The only true wisdom consists of knowing that you know nothing.

**DAVID:&nbsp;** Hey, that's us!

**CORALINE:&nbsp;** And me, Coraline Ada Ehmke, and we have a special guest today - Cameron Dutro. Hi Cameron.

**CAMERON:&nbsp;** Hello from San Francisco.

**CORALINE:&nbsp;** Cameron, would you like to introduce yourself?

**CAMERON:&nbsp;** Yeah, sure. I'm Cameron Dutro. I work at Lumos Labs. We make a product called Lumosity, which is an online as an online brain training app and sort of games. I've been doing internationalization work for, probably five or six years. I started at Twitter, and eventually moved to Lumosity, and yeah, just really excited to come talk to you guys today.

**CORALINE:&nbsp;** Awesome. I am very interested to hear how you got started doing internationalization but first, I want to ask, what is the difference between internationalization and localization. I think that's something that a lot of people kind of get confused about.

**CAMERON:&nbsp;** Yeah, that's a really good question. The way that I think about this is that localization is the process of translating text. You have some interface elements or some message box or something like that you want to translate, and that translation in Spanish or Farsi or whatever, is just basically a text replacement in most cases. So, you have the English text and then you have the translated text not because it was replaced in the UI element or message box or whatever it is, email maybe. So that's the process of localization, that's translating the text.

Then internationalization is the kind of, I like to call it "everything else" because there are a lot of other important things to do when you translate a website or a mobile app or something like that that are not necessarily just translation related. So internationalization for example, some of the tasks that come along with that would be equipping your application or website to be able to use translated text. There are other things like just making sure that your users are aware. They can see the website. It feels like a native experience to them.

So for example at Twitter, we did something kind of crazy for only translating the website into right to left languages so that would be Farsi, Arabic, Urdu and the whole website, if you go to Twitter.com and you select one of those languages, the entire website flips around on the vertical axis so basically it looks like it's being read from right to left, instead of left to right. So, does that give you the idea of what those mean?

**CORALINE:&nbsp;** Yeah, that's totally helpful.

**DAVID:&nbsp;** For our American listeners, how many people live in international?

**CAMERON:&nbsp;** Oh, my. Well, let's see, probably the majority of the world's population. Like in Twitter for example, I think, 70% of all of our users were outside the United States. So the US has something like 370 to 400 million people and if you think of the population of the world, as about six and a half billion, four hundred million is a drop in the bucket.

**CORALINE:&nbsp;** I've been to international. It's huge.

**DAVID:&nbsp;** Right?

**CAMERON:&nbsp;** Oh, I missed the joke. I'm sorry.

[Laughter]

**CORALINE:&nbsp;** That is important to bring up the fact that most internet users are not in the US. Yet, the websites that we frequent, the websites that we build as developers, the tools we use, even the languages that we write in are sort of English-centric, aren't they?

**CAMERON:&nbsp;** Yes, absolutely.

**CORALINE:&nbsp;** How bad of a problem is that you think, really. Is it a serious problem with people not being able to get access to information that they really need because of a lack of widespread internationalization? How much importance should be put on the issue?

**CAMERON:&nbsp;** That's a really good question. The companies that I worked at, a lot of the revenue goals that we have are rooted in having a product that can be reached by most of speakers of foreign languages. So Twitter for example, I mentioned 70% of the users are outside the US. The [inaudible] growth goals of Twitter were enabled by being able to reach people in other countries, in other languages. I think, that in many cases, somebody who speaks Chinese for example, would be hard press to use a website in English because not only is the language different, the character set is also totally different so they really can't even try. They would have to wait for that website to be localized in Chinese.

I think, it's also important to recognize that even the programming languages that we use, as a developer kind of community are all based around English. So all the keywords, and all of the looping structures, everything that we use inside a programming language are very much based around this English concept, so we say "if" and "then" and "while" and "do". Those things are English based.

To some extent, it's nice to have this kind of homogeneous language in which to communicate other developers. You can kind of think of like the language of mathematics in a similar way, when math is something that kind of transcends cultural boundaries, but it's not necessarily something that everybody can grasp right away. I guess, I think of translation is kind of the same way and programming languages is specifically kind of the same way. They kind of the lingua franca of being able to make something that, again, your computer can interpret and can do work for you.

So in that way, it's good. In kind of other ways, it's bad where it's more difficult as somebody who doesn't speak English. If somebody is a foreign language speaker, it's more difficult to get into programming, I would imagine because of that language boundary. When I was in college, I went to Peru on a study abroad program. With a roommate of mine, we went and asked a bunch of native Spanish speakers how they use technology, and we got to talk to a bunch of programmers. They said that it was definitely a little bit of a roadblock for them to learn programming because the words were not the same as they were, of course, used to speaking, and so, that limited however, they were able to get into the industry.

That being said, the Spanish and English were close enough, in terms of the grammatical structures that these programs were taught to. They had to have kind of gotten over that hurdle fortunately and they were helping other people do the same thing. You can imagine that if you have a couple of languages, if somebody speaks Chinese or Farsi or Hindi or something, and they don't necessarily speak English, it would be much more difficult for them to get involved in programming, and then across the internet at large.

**SAM:&nbsp;** Of course, even if they can understand the words, it's still difficult to type them on various keyboards because the characters are all Roman.

**CAMERON:&nbsp;** Yes, absolutely.

**DAVID:&nbsp;** I reviewed some code years ago that was written by someone from, I think, Brazil. He didn't speak Portuguese or Spanish, so Argentina, and it was a brain-bender. I speak English and I speak Spanish and I got presented with a program that was like, "If DNA_carro?"

[Laughter]

**DAVID:&nbsp;**"Carro. Period." You know, literally, it was like reading Spanish, but then there were these English language, you know: if, else, end if, while, do, loop, mixed in through, and then there would be comments and then the comments would just be just started rattling on Spanish again.

**CAMERON:&nbsp;** Yeah, definitely. I've seen that before as well. That's kind of brain bender.

**DAVID:&nbsp;** They are brain bender, and I actually, I haven't review code to this point, but I definitely dealt with text that is right to left, and that's huge brain bender too because when you're terminal, and maybe you're using some actual record model or something and you print out this Arabic string, but it's rendered in this super-strange backwards way, and by strange, strange to my sensibilities, right?

**CAMERON:&nbsp;** Yeah.

**DAVID:&nbsp;** To an Arabic speaker, of course, it would be totally normal, but that text, because of the way that English text like so Roman letters and Arabic letters are often arranged, they using a code - the Unicode Bidirectional Algorithm, determined what text direction should be for each individual chunk of characters. So you're like using your mouse cursor to highlight parts of the text, and highlights like in the backwards direction you're expecting. When you get to English text that highlights in the other direction and it's so confusing.

Not only it does happen in a terminal but it happens in entering text into a web form too. So it's one of those things where you just have to kind of like realize what you don't know, and to realize that you're going to adopt a different strategy for thinking about input, which is so fundamental to how I use a computer that it was really hard for me to grasp that at first.

**CORALINE:&nbsp;** We're very fortunate that no one uses hieroglyphics because hieroglyphics could actually be written right to left, or left to right, and you know [inaudible] to read based on which way the eyes were focused.

**DAVID:&nbsp;** The Chinese is written right to left, and then left right, and then right to left and then you can actually draw a box as you go, like if you're doing the verticals. Holy heck! Chinese is messy because over time, they would trade emperors and the emperor would say, "No rule!" Everything is written top to bottom, right to left. Top to bottom, top to bottom, and then the next emperor came in and said, "No." Left to right, right to left, left to right, right to left, and it changes, and whether you start left or right, or start right to left, it's important. The right way to do it changes depending on which century you're in. It's amazing.

So there's more of a challenge of you trying to do OCR is you look at a document and you have to figure out, "Okay, what century is this from?" because that completely changes. Is this is a guy who has turned blue or is just blue man group?

[Laughter]

**DAVID:&nbsp;** We don't know.

**CORALINE:&nbsp;** With the way the news has been lately, I often wonder what century I'm moving in.

**CAMERON:&nbsp;** Yeah, seriously.

**SAM:&nbsp;** Oh, there went my Esperanto joke.

**DAVID:&nbsp;** Oh! I was on Usenet back in the 90's and there was a guy there that spoke Farsi and he had done something absolutely amazing. This is a little bit of a war story which Katrina would frown on a little. But this is one of the cooler war stories, plus it's not my war.

Anyway, this guy spoke Farsi or Arabic, and back then, you had to stitch together your own fonts. The computer only had one font, and so what you had is you could actually go out to a memory location which was B00000 in memory, and that was actually on the video card. It was in video memory on the computer. You could change which bits were on and off to change which letter of the alphabet was switch.

So what this guy did is he went through, and he rewrote all of the letters on the keyboard to map two Farsi symbols so that he could get, I think, it was Farsi. I know it was a right to left language. But he mapped them all out and he wrote them backwards. He rendered them backwards.

Then, this is the cool part, he turned his monitor ninety degrees and stuck a mirror in front of it so the letters would be rendered in the right to left and his typing would come out right to left. That's how important right to left rendering was to this guy. At the time, I thought it was written hilarious. It was only later that I realized, "No, no. This isn't hilarious. It's important."

**CAMERON:&nbsp;** That's incredible. What a good story. I love to see a link to like --

**DAVID:&nbsp;** I will ask the Google.

**CAMERON:&nbsp;** Awesome.

**DAVID:&nbsp;** Obviously for reasons, this didn't catch on in the mainstream. So I think there's just this one guy hacking in his garage.

**SAM:&nbsp;** I was expecting you to say something like, "He hacked the display code so that it would actually print them right to left, but that's even better - using a mirror. That's a nice, simple, non-technical hack.

So I guess earlier on, I was wondering if there is any overlap between internationalization and accessibility issues but it seems like internationalization is fundamentally an accessibility issue in that. If your text is in English, most of the world ain't going to be able to read it. That said, I wonder if there are any overlaps. Are there ways that we can use internationalization to provide different descriptions of things? I'm just making stuff up here.

**CAMERON:&nbsp;** Yeah. I think, accessibility and internationalization, at least for me, they kind of fall into this category of altruism, I suppose. You know, like Wikipedia for example, they're a great organization to look to for organization that does good internationalization. When you talk to them about it, you feel this real sense of stewardship and altruism from them. I think, just about them in general, because what they're doing is collecting all human knowledge and giving it away for free.

But the fact that when you talk to their localization people, they're just very passionate about being able to bring that content to an international audience. You can definitely feel that in what their saying. I think, that's one of the big reasons that I enjoy doing internationalization and localization work because I know that what I'm doing is help and bring something that would have been inaccessible to somebody into their lives and making it accessible to them.

Accessibility is a very similar concept where it's something that somebody would not have been able to access before and you're giving them the ability to do that. So, whether that means adding ARIA-text for screen readers, or even outside of software, making sure that somebody who uses a wheelchair can access the building, your office building, or whatever, like all those things, are really bringing somebody into the fault who wouldn't have been able to get there before.

**CORALINE:&nbsp;** I make a point in several of my talks about open source. I sort of ascribe... I talked about the tragedy of the commons which I think everyone probably pretty familiar with. You have a village green, everyone's allowed to graze their animals there. If every person acts according to their own self-interest, they will grow their herds to the maximum size and consume all the available resources which of course, is bad for the community.

The analogy I draw to open source is that it's not the production of our intellectual output but it's a scarce resource but it's access that is a scarce resource and what our established systems of power and dominance and this includes cultural dominance are doing, are limiting the people who can even participate. That's the true tragedy of the modern common.

So, with internationalization, with accessibility, all these things can be used to enforce a class distinction or enforce a ruling class, if you will, of the internet of people who are English speakers, whether they're [inaudible] or not, it's a real tragedy.

**CAMERON:&nbsp;** Yeah, I totally agree with that. That maybe is kind of where that altruism comes from because you're giving people, at least in the case of Twitter and Wikipedia, you're giving people a voice that they wouldn't have before. I think people who, for example, Chinese speakers, they couldn't use Twitter beforehand, but they would have to speak English to understand the interface they could have tweeted in Chinese, I suppose.

But, yeah, that access is, I think, that's also a big problem just globally and also just in the United States, where a lot of under-represented minorities don't have access to a lot of things. They don't have access to education, they don't have access to food, and things like that. So, these people can be really invisible.

I quote to back to internationalization here, and I say that a lot of developers I think they don't think about how their futures and how their audience is more than just people that are like them. If they're English or they speak English natively, they're building a website for other English speakers, they don't often think beyond that, and I think, that could be dangerous.

**CORALINE:&nbsp;** Yeah that's the thing that comes up a lot with discussions of diversity. Diversity can solve diverse problems because if you have a team that is homogeneous, they are only aware of the problems that face their particular community or demographic, and they're unaware of the implications of the things they write for people who are different from them.

**SAM:&nbsp;** And then you wind up with things like Facebook's real name policy which is problematic for a number of populations.

**CORALINE:&nbsp;** Try changing your name on PayPal, if you're trans. Good luck with that. They actually tell you to cancel your account and start a new one because it's impossible. That's their actual recommendation. You cannot change your name on PayPal.

**DAVID:&nbsp;** Cancel your account and create a new one. That --

**SAM:&nbsp;** I do the first step.

**DAVID:&nbsp;** That seems almost violent to me.

**CORALINE:&nbsp;** I think it is, by some definitions that it's a form of violence. I totally agree with you, David.

**DAVID:&nbsp;** Right? I need you to cease to exist and come back as a different person.

**CORALINE:&nbsp;** I just saw the... Never mind. I don't want to go off tangent. But I have horror stories.

**SAM:&nbsp;** But it all does come back to either developer ignorance or indifference, or maybe even if there is a developer on the team who is advocating for this stuff, it's hard to get the product manager or the business side to greenlight the time spent doing it.

**DAVID:&nbsp;** In agile, we pride ourselves on doing the important thing first. What is the most important thing? Well, the reality is the product owners end up stack ranking all their features based on "Are they worth it?" And "worth it" is a calculation of how much perceived value divided by how much perceived cost. We know how much it's going to take to internationalize or localize. If you have a whole bunch of white dude sitting around and writing the code, they're going to, "Well, you know, they can speak English." There's no perceived benefit here.

**CORALINE:&nbsp;** I take exception on one thing you said there, David. I don't think that, as developers, we do know the cost of internationalization and localization because it's --

**DAVID:&nbsp;** Yeah, it's true.

**CORALINE:&nbsp;** -- Most of us even do. So, Cameron, I noticed that you created a couple, or you've been involved in creation of a couple of tools or txgh, and something called Rosette, and I take it that one of those is more or less a library, the other one is more or less a service. Can you talk about this a little bit?

**CAMERON:&nbsp;** Yeah, totally. [Inaudible] in chronological order. When I was working at Twitter, we had this thing called the Translation Center, and it's translate.twitter.com. It's a crowd sourced platform so anybody can go and sign up for an account there, and use the tool to translate the website into their language, and there's a bunch of moderator tools and stuff that are built into it.

It's a pretty cool platform, and when I was working there, I noticed a couple of problems with it, and problems that the organization isn’t really interested in solving, just because of resource allocation and whatnot.

When I left Twitter in 2014, I thought, I can probably take a stab at fixing these issues. So when I joined Lumosity, one of the things that I said I'd like to do when I was working here was to build a better internationalization platform, or localization platform. They were like, "Okay, yeah. Sure, we'll let you do that."

So, I sort of working on Rosette, and Rosette is like a service, it's also like the library, it's really a bunch of different smaller libraries put together into one. So you can figure this thing and then, it helps coordinate the translation of your content. What it does is it checks and uses a library which is actually built on JRuby, and uses a Java library called JGit to notice when Git has changed, that causes the change and that change will contain changes to your translation files, and [inaudible] will notice that, and then take those translation files automatically move them up to some translation service which of course, in Twitter's case, would have been the translation center.

But in other people's cases, sort of the company's case, a lot of companies will contract with companies like Smartling or Transifex or Lionbridge which are translation vendors and they have their own tools that help translate content so they interface for translating the content and they kind of manage that whole process for you. So Rosette is just the backend that connects GitHub to these translation services.

So, Rosette was the first stab at kind of doing that, and users get attracts everything via the [inaudible]. So, like an individual phrase that comes from the translation content, so in Rails that would be something like en.yaml, that thing config locales, en.yaml. It takes that content loosen up there, and then attaches the [inaudible] to that, and when you going to download your translations, it says, "Okay, so what was the last time this file changed?" These are Git magic to figure out when the last time that file changed was and then it goes into the database of translations that we had, pull those out, and delivers them to you.

So it's a very dynamic system, and it was something that we used for a long time. We eventually kind of realize though that it wasn't exactly what we needed. It was a little too much, little too complicated. One of the big reasons for that was because we were using the translation TMS system, a transition vendor system called Smartling, and they didn't have a super-well, fresh-out API so we had to do kind of a bunch of little tricks to download that what's called the translation memory, which is a big XML file and parse that, and get strings out of it, and there's a lot of complexity. It was kind of built into Rosette, to specifically, to one of the Rosette gems.

So, we realized, there's got to be an easier way to do this, and so looking we were looking around, we found this other tool that was initially built by a company called Strava, and we had heard about it kind of through one of my industry contacts. The guy said, "Well, you know, we've been building this thing and it's really working for us for a while now. It's called txgh, and "tx" for Transifex and "gh" for Github.

So, Transifex being basically another translation management system like Smartling, just an alternative to that. We were switching to Transifex at the time, and so we said, "Oh, you know, let's get this thing a shot." At that point, Strava had transferred control of this txgh to Transifex and then we forked it and started working on it, to improve it, to add some features [inaudible], and kind of at this point, I think, we're probably the major contributors, the biggest contributors to txgh. Also, probably the biggest users of it.

So it's like we had it kind of iterate on and that's one of the things that I want to bring up and that is that internationalization is really not a feature. Internationalization is a process. So we talk about continuous integration, we talk about continuous delivery, and what I'd like to kind of coin here is continuous localization, and that's what txgh and Rosette are created to do, to constantly look for changes in your translations and push them up.

**CORALINE:&nbsp;** Yeah, in your pre-show materials, you talked about [inaudible] processes, and it seems to be right in line with the way you're describing a good internationalization or localization process happening is that it is tied to development cycles, it is all those things?

**CAMERON:&nbsp;** Absolutely.

**CORALINE:&nbsp;** How feasible is it for a small company without a lot of resources, maybe without a resource to devote to internationalization that actually get their website or the web application, trying to it and keep it translated.

**CAMERON:&nbsp;** That's a great question. I think there are a couple companies before, and never actually bootstrapped a company from zero to transit. So my answer is going to be little tempered by that. But kind of just the tools that I know in the Ruby on Rails world, they're fairly easy to learn, the processes is not hindered necessarily by the tools. It's really hindered by, I would say, in time that you take to do your website or your mobile app. Because the process of integrating translations can be time consuming, and kind of tedious process.

For small company, it would probably take, and again, this is going to depend on the size of the app, and size of the website but I'll probably budget a couple of months at least for doing the initial work and then, when it's to be integrated into your site or mobile app, then it's time to kind of go into that maintenance phase but that maintenance phase is going to be very active. So you need to constantly make sure that something that you thought was translated is now translated, all that content pushed up to your translation management system so there needs to be some stewardship there, some maintenance there as well, to make sure that continuous localization happens. It's worth saying that the upfront cost might be a certain number of months, but then you also to be just willing to maintain it for basically the entire left of the product.

**CORALINE:&nbsp;** How feasible is it to crowdsource translation?

**CAMERON:&nbsp;** For Twitter, it really was a great solution because the users of Twitter were just very, very passionate people, and they still are to this day. We had one translator who... the site was not even available in Chinese, but he went into translation center, and they hacked the URL. He changed the locale and the URL to Chinese as zh... I think it was zh-cn he changed it to. He went through and translated like over 10,000 phrases in like a couple of hours, and he realized after he had done this, he actually put in the wrong locale. He wanted to put zh-tw and so he went back and hack the URL again, and translated all 10,000 of those phrases again. So, in a 24 to 48 hour period, he's translated like 20,000. Yeah, that was crazy.

He was obviously just a very passionate Twitter user. He really wanted to see what website in his language. He wants to bring it to his friends that maybe didn't speak English. He also went to Google Trends and checked his translations, and he's actually doing this. He's actually just pounding out these translations one after the other. That kind of passion, that kind of drive, that kind of user base is really a good candidate for doing outsourced translations and that's why it worked for Twitter. I don't think that it works for every platform. So, platforms like Twitter, like Wikipedia, maybe like Facebook. Facebook actually has inline translations, so you can go to Facebook and let you translate an entire interface, kind of becomes live. You can click on individual pieces of the interface, and translate them. They have separate tools for that and works for that really well too.

But for a company like Lumosity, and maybe smaller companies out there, there's not that rabid user base who is just very, very interested in translating the website and mobile app. so for those, I would say that most of the time you want to go with a translation vendor. You know, somebody who is able to sell you the resources to translate.

**SAM:&nbsp;** Sure. So what I'm hearing there is that if crowdsourcing is an option for you, you're popular and successful enough that you can afford to hire somebody to do it.

**CORALINE:&nbsp;** I think that's really the case. I had a quick experience with translation earlier this year, with Contributor Covenant - the open source code of conduct. Someone posted an issue and saying, "Hey, why isn't this available in other languages."

And I was saying, "That's a great question." So I put out a call on Twitter for translations and within a month, Contributor Covenant has now been translated into sixteen different languages. My rule was that it could not be the work of a single translator. Someone else who is a native speaker had to review the translation to make sure that the nuances were there. It was an incredible effort that the community put forward, and I was so thankful and so humbled. So you know something that's possible. People are good, sometimes.

**CAMERON:&nbsp;** Yeah, that's a great example. That's very cool. Congratulations that the community was able to rally to do that. That's very cool.

**CORALINE:&nbsp;** Yeah. I was really impressed. That was very great.

**CAMERON:&nbsp;** Maybe for projects that are just kind of inherently open, and Twitter got a lot of flak recently for not treating their developers very well, and other things like that. But the platform still remains, a really cool platform. It's very dynamic, it's got a lot of individual people speaking on it, there's a lot of people that voiced says totally free. That being said, I think that's why you get the number of people who contribute that way they do on the translation center. And sounds like the, you say, was the open source code of conduct?

**CORALINE:&nbsp;** Contributor Covenant, yeah.

**CAMERON:&nbsp;** The Contributor Covenant, I'm sorry, yes. So that right there also obviously, it applies to so many people and I'm sure a lot of people are very passionate about that so they were to dedicate their time, and kind of like Lumosity really doesn't see that kind of engagement, I guess.

The platform is still a great platform. The games are fantastic, and I really believe in our mission. But it's a product that people really buy. It's not a product people would use to communicate with other people. So, it doesn't lend itself really well to that crowd source translation techniques.

**SAM:&nbsp;** A little bit earlier in the show, several of us went looking for a wonderful blog post called Falsehoods Programmers Believe About Names which is wonderful and will drop the link into the show notes. But I was wondering, how do internationalization issues affect database schema design? I mean, I know that how you store names and phone numbers is important. Are there other gotchas that was sneaked in there?

**CAMERON:&nbsp;** Wow, that's a great question. So, you said, the database schema and I'm looking at this article now. I haven't had a chance to read it.

**SAM:&nbsp;** The idea being that not everyone has first name, middle name, last name, or part of it or name at all.

**CAMERON:&nbsp;** Right.

**DAVID:&nbsp;** That article, they get progressively harder like everyone had a single, unique identifying name. Everyone has a single first name, middle name, last name. Everyone has a name that can be represented in just one character set. It ends with people have names, and somebody called them out, and says, "Oh, come on! Everybody has a name."

Can you get a counter-example? And list like two or three examples of people who don't have names. What do you do with the system, we've bought into the falsehood so hard that we are blind to the fact that we have bought into it. We have an entire body of work based on whether or not someone had a name in English speaking world, right? We call that person a "John Doe". Right? The reason you have "John Doe" or "Jane Doe" is because you have a form that is relentless. You must type in a single first name and a single unique last name for this person, and I love saying question about database schema because all the international... I just realized, you just totally caught me flat footed because I'm realizing that, "Yeah, I would use the same schema," and then internationalization is just a translation layer on top of that to translate things to and from America.

**CAMERON:&nbsp;** Yeah, that's a really interesting article, and I'm enjoying it. They list the number of the things he had on his list, then the one at the bottom is the assumption that people even have names. That's really cool. Yeah, I haven't considered this before, or dealt with that before. That's just one of my blind spots. Clearly, I just have never talked to somebody who didn't have a name.

**DAVID:&nbsp;** The person who challenged the people has names things, come on! The person who was a John Doe had a name, we just don't know it. He said, "Can you give me an example of somebody who doesn't have a name?" And it's like, "Well, lots of infants are born and never named," and then he gave a really terrifying example which was a fully grown woman born in Somalia, born into slavery, never given a name, all the way to adulthood, never has a name.

**SAM:&nbsp;** So, since I asked the question, I should at least punt our readers to something to read about it, or pardon me, point our listeners to something to read about it. Carina Zona for a number of years is giving a wonderful talk called Schemas for the Real World where she talks about some of the implicit cultural biases in the way you design your database.

**CORALINE:&nbsp;** I love that talk. It also touches on some gender issues as well. The myth that sex is a dropdown failed.

**SAM:&nbsp;** Let alone a billion.

**[Laughter]**

**DAVID:&nbsp;** Now, come on, it's getting crazy. They used to be just a Boolean, right? Then, you said we couldn't have the gender binary. You took that away from us, and now, you're saying we have to give you --

**SAM:&nbsp;** You're not content with the list --

**[Cross-talk]**

**CORALINE:&nbsp;** Pre-form text is the correct way to solve --

**DAVID:&nbsp;** Can we just say, "Other, please specify?" No, that's --

**CORALINE:&nbsp;** That's othering.

**DAVID:&nbsp;** Yeah, it's literally othering. Isn't it? Literally othering. Okay, fair enough. It's humor territory, and then it hit too close to the bone. Sorry about that.

**[Laughter]**

**CAMERON:&nbsp;** I am curious, so for drop down for sex, what's the appropriate --

**CORALINE:&nbsp;** Pre-form text is the best way to solve that problem.

**CAMERON:&nbsp;** Okay, make sense.

**CORALINE:&nbsp;** And Corina goes into that inner talk about the common concerns about that. What about normalization? It's like actually it's not that hard of a problem to solve when you look at the range of input values, and you're able to make some decisions about how that data breaks out, and still do some programmatic analysis of it. It does not break your analysis.

**DAVID:&nbsp;** That was going to be a very next question, is that, it's well good to allow somebody to specify male, female... I don't know. I don't know what the other options are. But if you let somebody type something, and we're dealing with, [inaudible] we deal with patient gender, and some of our customers out there are using a free form field in it, it gets tricky. The people listening to the show, there's going to be somebody in marketing that's going to say, "Yes, but how do I know which color of shoes to try to market to you if I don't have [inaudible] and feel to swap on," and I like what you said about it doesn't break analysis.

**CORALINE:&nbsp;** Yeah, I mean you can simply ask people what their preferences are. Do you want to see advertising that is targeted to women or do you want to see advertising that is targeted to men? You can ask that question without asking anyone to out themselves with regards to their gender identity.

**SAM:&nbsp;** Right, there's --

**CORALINE:&nbsp;** Could you ask someone what their pronouns are? And so making tacit assumptions. We cut [inaudible] a little bit. But --

**DAVID:&nbsp;** I have one job here. Let's stick this off into the weeds. This means are important, though. I mean --

**CORALINE:&nbsp;** They really are.

**DAVID:&nbsp;** I'm going to say, they're really cool, and I don't want to trivialize them. They are cool. I don't mean that in a trivializing way. I mean that in a sincere way. This really is kind of the heart of I18n, l10n. That sad when it's actually easier to say the numbers than actually saying the word, isn't it?

**CORALINE:&nbsp;** It's interesting because programmers would like to say, "Oh, I like to solve hard problems," and we're faced with some very concrete hard problems like I really don't know anything about internationalization. I really don't understand this whole gender thing. It's like you'll spend a weekend to learn Haskell, but you won't spend a weekend to learn best practices for internationalization. Seriously?

**DAVID:&nbsp;** Programmers don't want to solve emotionally hard problems. They want to solve intellectually challenging ones.

**SAM:&nbsp;** And that's not intellectually challenging?

**[Cross-talk]**

**SAM:&nbsp;** -- Take out you guys.

**DAVID:&nbsp;** I would rather work on a Rubik's cube all day, than try to confront gender identity issues, right? I'm sorry, I spoke in first person, and I was using that as like the implicit "we" there. I'm not saying, I genuinely feel that way. But it's easier to figure out, "How I'm going to use the framework of this on top of Rails... “That’s clean and it's emotionally tranquil and sterile and it's safe. I can --

**SAM:&nbsp;** And you know when we're done.

**DAVID:&nbsp;** And we know we're done.

**SAM:&nbsp;** That sort of false feeling of security that, "Oh, we've solved this problem now. It will not trouble us again."

**DAVID:&nbsp;** Yes, where like the hard emotional problem, you don't get that.

**SAM:&nbsp;** What you get is more problems.

**[Cross-talk]**

**SAM:&nbsp;** -- You get new harder problems that, first, you had to deal with one thing, then you extended your understanding and now you see other places where you can go and learn.

**[Cross-talk]**

**CORALINE:&nbsp;** -- For human problems.

**SAM:&nbsp;** Well, that too.

**DAVID:&nbsp;** Hey, didn't we have a guest, at some point?

**[Laughter]**

**CORALINE:&nbsp;** Hi, Cameron.

**DAVID:&nbsp;** Hi, Cameron. Welcome back to the show.

**[Laughter]**

**CAMERON:&nbsp;** No, this is great. This is awesome. The discussion is totally awesome. I wanted to say that I agree with the idea of [inaudible]. One of the things that I learned from this show is that software is about people, not processes. It's not about coding. We definitely have perspective that I hadn't had before, [inaudible] the show. Especially in a lot of the recent episodes.

Now, I'm sort of looking at all of these internationalization problems that ideally, it kind of on a daily basis, and thinking like how people oriented. Like if we were just working with computers all the time, we wouldn't have to internationalize anything because everything the computer can understand is ones and zeros. So, that are very clean, they're very easy, there are no emotions involve, but the fact that people don't speak in those languages, don't speak in ones and zeros, mean we have to write [inaudible] in order to write language in the source code. Now source code gets compiled or interpreted.

That's kind of the same thing that we're doing for people who don't speak English. We're helping them then interpret this content that we have in this other language that they speak. So, there's kind of parallel to be drawn. I'm not doing a great job of drawing it, but --

**SAM:&nbsp;** The picture that I get from that is that maybe if your website is an English-only, it's like you've written your code in assembly.

**CAMERON:&nbsp;** Right.

**DAVID:&nbsp;** -- On one machine.

**CAMERON:&nbsp;** Exactly, that's a really good way to put it.

**CORALINE:&nbsp;** I think, we've done a pretty good job of underscoring why internationalization is important and some of the mechanics involved in getting started with internationalization but what if I am a developer and I've never really thought about this before, and I want to educate myself on the topic. What are some resources that I could start looking at to get up to speed with the current state of internationalization?

**CAMERON:&nbsp;** I'm coming at this from a Rails perspective. I think that most people, when they come at internationalization they're [inaudible] so from the concept or from the perspective of a framework, so whether that's Rails or Django or some JavaScript framework, or iOS or Android, they all generally have this concept of internationalization kind of built into them. That's not always true of course.

But if you took the Rails example, and I've mentioned that there are yaml files you translate. So, en.yml would be the English version and es.yml be the Spanish version, and Rails has a pretty decent I18 guide, so the Rails guides - great resource, really just in general for learning about Rails - but they have one for internationalization that's pretty complete. That's a great resource to start with, and just based on whatever framework you want to use, whether that be the Django or iOS or Android, there are also guides for those. So, Googling for those will reveal them.

They all kind of have their own kind of quirky way of doing it. Rails uses yaml files, Android will use XML files, and iOS uses this proprietary dot-strings format. I'm not sure what Django uses. I want to say, it's JSON. I'm not sure. But all these different formats, usually the translation manual says let you choose. We'll have that support for that format available.

But you wanted to learn like some of the nitty-gritty details about internationalization so this is kind of beyond localization. There are a couple of tools out there that you can use for that and the main canonical ones are ICU4J and ICU4C, and these are made by the IBM Corporation, so in a big company and a very business-like or whatever, they produced this really amazing software package called ICU or International Components for Unicode.

They have Java Version and they have a C Version. So a lot of frameworks out there, speaking specifically now, I guess, with iOS and Android, they use ICU4C. It's an interface available or an API available in your mobile apps to translates dates and times, and just sort list of internationalize words. For example, Russian words are sorted in a different order than they would be, if you're just using the ASCII or just their code point sorting representation. There are tools that are doing that. That's what ICU does.

What I have done also is work on a project when I was at Twitter, called TwitterCLDR, which is basically an ICU port for Ruby. CLDR stands for the Common Locale Data Repository which is a huge collection of data for internationalizing the content of website and mobile app. It's a bunch of XML files that are porting it to JSON. As we speak, I'm trying to get that coordination I worked in.

But seems there's a really cool kind of resource, it was a very technical resource and all these files, they contain things like how to format dates, and there's list of currencies that are available in their website. They have translations kind of baked into all these XML files for all these different currencies you might want to pay with. They have translations of language names so if you want to say Spanish in Spanish, you say Español. There's a ton of different things in there, and ICU is I think, the major consumer of CLDR data, and so is TwitterCLDR.

It's like finding a good library for doing these things. Also I think, like another kind of big step forward, and you can learn a lot, I think, by reading the TwitterCLDR readme and also the readme for ICU and list of websites. They have set up for that. There are a lot of different interesting tidbits you can glean from those, and you may not even realize that translating a date is sometimes difficult, or translating a time stamp is much more difficult, or sorting a list of text or segmenting text because there's a lot of language doesn't use spaces. How would you segment text in other languages?

So it's like that kind of thing. I'm trying to kind of just get a handle on the things that maybe you don't know that you don't know, that would be a great way to [inaudible] level up in the age and space.

**DAVID:&nbsp;** That is awesome. Cameron, you mentioned at the top of the show that you can go into like Twitter or is it Facebook or is it both, and you can switch your language to Farsi and it will actually rerun the page right to left versus left or right. I mentioned earlier on that 25 years ago, this was a bone-breaking technical challenge. I mean, like literally you would have to like [inaudible] things to make things scan in a different direction, and kind of thing.

Because these things were embedded in the bios which was in the hardware of the computer that you were not just going to change something in the operating system and get away with it. What do you do now? I think there might be some people listening to think, "Oh, you switch your English to Farsi, and we give you a whole new front end." And I'm guessing that we don't, that we've come such a long way now that we can actually just send something down the pipeline and said, "By the way, we're into everything right to left now." Do you know what's technically involved with that kind of a change?

**CAMERON:&nbsp;** I do a little bit. Like a lot of it is CSS. So there's a --

**[Brief silence]**

**DAVID:&nbsp;** I was going to make a joke that it's a CSS3 flag. That's awesome.

**CAMERON:&nbsp;** Yeah, it's not one CSS3 flag. I mean, CSS does have now the, I think, it's bidirection. They have that CSS property now. That helps significantly when it comes to text rendering and things like that but these things that are just applying to each individual element. So like for example, the page has a CSS, like a container [inaudible] around it. So, the CSS for that pages is inside that container, you have some float right, some float left, and you'll just like swap those float rights and lefts. It's that kind of idea but it's not just one CSS property, thank God.

But it would be awesome at once because it will be so easy because just add it, and you'll be done. The browsers, like generally speaking, browsers have a lot more support for bidirectional language than they used to. The CSS direction, that actually, maybe a CSS3 property, the bidirection. I'm not sure though. Maybe it's been around for a while. At least now, it was more supported in browsers.

**DAVID:&nbsp;** In my opinion, CSS jumped the shark when Google added a skew to their search. If you haven't seen this, do this right now. Just open up Google, and type in askew, A-S-K-E-W, and just hit enter, and then watch your brain explode.

**[Cross-talk]**

**[Laughter]**

**DAVID:&nbsp;** Google will mess with your head, and I actually really happy to see this. Now, Googling "askew" is freaking awesome. But I'm really happy to see people using this power for good now, instead of just for weird.

**CAMERON:&nbsp;** Yeah, totally. Here's another do a barrel roll trick. You type "do a barrel roll".

**SAM:&nbsp;** Oh, yeah, that's great.

**DAVID:&nbsp;** -- Googling something.

**CORALINE:&nbsp;** My favorite one is Conway's Game of Life.

**CAMERON:&nbsp;** Oh yeah, that was great. Is the one with the [inaudible]?

**CORALINE:&nbsp;** It actually does. Conway's Game of Life, it takes away your Google screen.

**CAMERON:&nbsp;** Oh, there it is. Oh, that's awesome.

**DAVID:&nbsp;** Do a barrel is beautiful.

**SAM:&nbsp;** Okay, I know, we're fully distracted.

**[Laughter]**

**DAVID:&nbsp;** If you could you ship some riddle into our houses, please, before the end of the show. Thank you!

**SAM:&nbsp;** So, Cameron, is there anything else we should talk about before we go to picks?

**CAMERON:&nbsp;** There's one thing that I'd like to bring up and I haven't gotten the chance to yet, and that is talking about Unicode. So this is a pretty deep technical topic. I don't know if it's okay. Because if you like to go into that, we can, actually.

**DAVID:&nbsp;** Do it.

**CAMERON:&nbsp;** So, Unicode is this standard developed by this body, this... what they called, [inaudible] a foundation that is really how text is displayed online and in mobile app. It's basically like ASCII. It's a one-to-one mapping between what are called code points were just numbers, and actual textual characters.

For example, The Unicode Consortium. David put it into the chat. Yes exactly. They're kind of the arbiter of all these things. Most people know the Unicode Consortium, if they know them at all because of Emoji. Emoji are, of course, these fun little images you can put in your text messages, and The Unicode Consortium are the kind the arbiters of deciding what goes in Emoji next.

One kind of cool side note, one of the things they just did recently was provide... so for some of this Emoji, they had people's hands, or faces. They had recently added the ability to provide different codes for different shades of people's skin. You don't always have to get stuck with the white person's face. You can choose the slightly darker skinned face or the black person's face, and it's something that they have recently added.

So, The Unicode Consortium, I'm just saying that they're pretty cool. They definitely like embraced this whole kind of crazy Emojis that people... You know most people don't really care about Unicode. It works on their website and their mobile app, and they are like, "That's great." But Emojis are kind of one of these quirky things that they now adopted as well in our [inaudible].

Back to what the Unicode is, it's this mapping of characters. But instead of just handling characters from A to Z, Unicode handles characters across just about every kind of written language that is in the world currently. It supports Cyrillic characters and all the Chinese characters, all the Japanese characters, Korean, Hindi, Khmer and Lao, and all that stuff. All those characters are now available to type on a keyboard because of The Unicode Consortium.

Before this other standards bodies existed that tried to make kind of their own formats for international text so Shift-JIS is one that's was popular for Japanese text. The problem with these, though, is that they weren't complete and they were all kind of had... you look at these different sets of code points, they would have overlapping regions, and they were difficult to encode in between. But as a Unicode set, we could take all of these code points and we can merge them into one unified set and then hopefully that can get adopted by everybody who wants to use text on the internet.

For the most part, that's happened. I think, that we've, as an internet society, we've migrated from ASCII and Shift-JIS, and all this other kind of smaller formats, smaller code point mappings, we've moved from that to Unicode now. I think that has only done great things for the internet specifically, and also just for texting read on a computer anywhere. So your terminal now supports Unicode, websites, mobile apps, all that stuff.

**CORALINE:&nbsp;** There's a great article in Model View Culture a little while back by a woman name Aditya Mukerjee called I Can Text You A Pile of Poo, But I Can’t Write My Name.

**[Laughter]**

**CORALINE:&nbsp;** Which is actually a critical of Unicode --

**[Cross-talk]**

**CORALINE:&nbsp;** Yeah, she's being critical of the Unicode Consortium because her language which was Bengali, is treated as the second class citizen on the internet. Until 2005, Unicode didn't even have all the characters from the Bengali alphabet. Her example was if you want to write the words "suddenly", you had to combine three separate unrelated characters into sort of a convention. Sort of like spelling out "W" with slashes, and even today, when she wants to write her own name, which is not only a common Indian name, but one of the top thousand names you [inaudible] as well, the final letter in her name still doesn't have its own Unicode character.

**CAMERON:&nbsp;** Oh wow. Yeah, that's unfortunate. I do know The Unicode Consortium is constantly revamping the code point set. The fact that they are a consortium, they're kind of a committee, I guess. Those were the stewards of the standards. But it's a good point that you make, Coraline, that, it's still a lot of work to go. We've definitely not done with the set yet.

**CORALINE:&nbsp;** Yeah, it's not a solved problem yet.

**DAVID:&nbsp;** No, definitely not.

**CAMERON:&nbsp;** It's is worth noting that it has made great progress. I guess it's my point. There's been a lot of progress made because when I was on the internet for the first time in probably 2001 or something, when I was like twelve years old, the only character encoding that existed was, I think, was a Western... I think it was called Western Encoding or something, which is basically ASCII with a couple accented characters. You know, Unicode really existed but it was not widely adopted. At least now we have this framework for defining other characters.

**CORALINE:&nbsp;** This is been a really great conversation and I really appreciate you coming on the show. We're going to do picks now, and then you'll have a chance to say goodbye. So, David, do you want to start off with some picks?

**DAVID:&nbsp;** You bet. I've got lots of fluff and no stuff, I guess. Back in 2008/2009 when I really got into Ruby on Rails internationalization, localization, minimization which are I18n, L10n, M10n were all the rage. Everybody was excited about this and so we really were taking words and intranumeralizing them. So if you're born after 1998, you might not know that I18n is just...it's because the word internationalization is 20 letters long, and if you take the "I" and the "N" off, you have 18 letters left. So the abbreviation is I, 18 letters, then N.

**CORALINE:&nbsp;** That's accessible.

**DAVID:&nbsp;** Yeah, that's accessible. Yeah exactly, and it fits in forty bytes. Anyway, I must be using MCBS, or... Anyway, I got so wound up about this that I ended up writing a code snippet called I17n, and Cameron was telling me before the show that I should convert this into a gem. If I do that before this goes live, I will post a link in the show notes to the gem.

**SAM:&nbsp;** That needs to be on NPM now.

**DAVID:&nbsp;** Yeah, exactly. I17n is of course the word intranumeralization which is 19 letters long so when you take the "I" and the "N" off, you got seventeen letters left, and all it does is take a string, give you back the first and last letters, and then the number of things. So my name becomes D3d, which is kind of cool. It's is one of my private repositories in a directory called "stupid" so you're just forewarned.

I have another pick but I can't remember what it is. Oh, I was going to pick the Falsehoods Programmers Believe About Names and we already mentioned that in the show. There is my picks.

**CORALINE:&nbsp;** Awesome. How about you, Sam?

**SAM:&nbsp;** Yeah, I think, I'll just do one today. The fellow people who have been on the call with me might have been wondering why I'm sort of antsy on the video, and the reason is this thing called the Mogo Seat. It's sort of like a monopod for your butt. There's this extensible aluminum bit like a cane. At the bottom of that is this big round rubber squishy thing that sits on the ground, and then at the top, there's just this thing that's shaped kind of like a pelvic down. You sort of lean back against this thing, and it turns you into human tripod. As ergonomic equipment goes, this is reasonably affordable. It's a hundred bucks. It lets you sort of move around a little bit more naturally than you might if you're in a chair. I find that it helps me stay at a standing desk longer than I would, if I were just on my own two feet. That's my pick. That's the Mogo Seat, and I'll put a link in the show notes.

**CORALINE:&nbsp;** Awesome. I have a pick and I want to share a couple picks. The first is a talk by Schneems, from RailsConf 2016. The videos are available now. It's called Saving Sprockets. He kind of had it gimmicky, him on stage, dressed like Indiana Jones, and kind of doing an Indiana Jones skit, but the talk was pretty serious.

It talks about what happened when Joshua Peek made him of Sprockets left the project. He covers some really interesting points about like transition planning for an open source project, and the fact that you might feel betrayed when the maintainer leaves. But maintainers don't actually owe us anything but we do owe them respect. He talks about how the act of helping out with an open source project helps to retain and create new maintainers and basically, it's about acknowledging that maintainers won't be around forever, and how can you prepare accordingly. He shared the video of the talk on his blog, and he has a transcript available as well. I'll post the link to that in the show notes.

The second pick today is a game. If you know me in a while, I don't play games very often. I have a hard time getting engaged with games, but this one is kind of called my interest. It's called Calvino Noir. It's on Apple's Best of 2015 list. It's a game with a film noir setting which is probably why it appeals to me so much. You control three characters. Each with different abilities and you're moving them through these beautiful sets of 1930's architecture, and the whole game in shades of grey. It's a mystery plot that requires conspiring with multiple characters and the main character provides a voice of a narration, just like from [inaudible]. Seven levels, three acts, very well voice acted. It's available for MacOS, and iOS. It's available on Steam, and for the PS4, and that's it. Calvino Noir, that's my pick.

So, Cameron, what are your picks today?

**CAMERON:&nbsp;** Well, I'm a little disappointed that I wasn't on a podcast with an epic D Brady hot sauce pick. But, I guess --

**DAVID:&nbsp;** Okay, so teaser. I am tracking down a friend of mine... I do have another friend of fine. Well, yes, a friend of mine...

**[Laughter]**

**DAVID:&nbsp;** I do actually have friends, people. They just wouldn't admit to it. Anyway, a friend of mine introduced me to a gentleman a couple weeks ago who mentioned a hot sauce - I can't remember the name of that. I'm trying to get back in touch with this guy to track this person down. I'm actually hunting down a rare sauce for you guys right now, and because he gave me a very specific food pairing for it that was just mind blowing. I am working on it. I promise. We we're working tirelessly behind the scenes.

**CAMERON:&nbsp;** Okay, for my picks today, I'm on a lump kind of three different things into one pick. That's for ICU and CLDR. So, these data sets are very, very cool data sets. It's amazing that they exist. It's amazing that a company like IBM and other companies like Google, and Apple all contribute to these things to make the state internationalization better across, basically, all software.

What I want is pick ICU and CLDR and ICU is something that's written by IBM. They maintain that project. CLDR is written and sets contributing thing that lot of companies contribute to and I put links to those as well on the chat here, and hopefully they can put it in show notes.

Then also, the gem that I have collaborated on with a number of other people called TwitterCLDR, there's a Ruby version of this, and a JavaScript Version of this. They're available on GitHub, and they're basically just port of all these internationalization features from ICU to Ruby and JavaScript.

Another pick I want to do is fun kind of game pick and it's a game called Hacknet. I was told by a coworker about Hacknet. If you ever play Uplink, it's kind of a modern version of Uplink.

**SAM:&nbsp;** Oh, cool!

**CAMERON:&nbsp;** One of the cool things about Hacknet, though, whereas in Uplink, you would click buttons and there was not a lot of technical meat to it. Hacknet kind of tries to mirror as much as it can kind of the real world of using a UNIX terminal. So you hope you'll open up the game and you have available to commands like "cd" and "ls" and "cat". The commands do what you expect them to do as a files system, you can look at the bin folder, and you can scp files - literally the scp command, you can scp files to your own workstation. It's kind of a nerdy version of Uplink and I've been really enjoying playing. There's a campaign and a storyline that goes along with that. So, I have a link for that as well. Probably you can buy in Steam Store, I think, it's only \$5. It's pretty affordable.

Then the other pick I have, and I have to pick this because it's something that's close to my heart now. I'm a Golden State Warriors fan, and I don't want to alienate your listeners who are maybe Cavaliers, or Thunder or Trailblazers fans, but those are professional basketball team, and they had been very well this year, and I really enjoyed watching their games, so go Warriors.

**CORALINE:&nbsp;** I had a conversation recently where I decided that I would be really interested in sports. If the teams were actually made up of what their name say.

**[Laughter]**

**CORALINE:&nbsp;** I love to see Warriors fight Giants, like I would go to that. I would totally do that.

**DAVID:&nbsp;** Their names are so... they're so not what they actually are. Although, they happen... they have been battling this year for the top spot.

**CAMERON:&nbsp;** I guess, you can see they're... they're Warriors in a metaphorical sense.

**CORALINE:&nbsp;** My daughter points out that the most boring game would be between the Sox and the Sox.

**[Laughter]**

**CORALINE:&nbsp;** Sox playing out on the field or something. All right. Well, Cameron it's been really great and really educational talking to you today. Thank you so much for coming on the show. We've had a really great time, and I hope you enjoy to this, as well.

**CAMERON:&nbsp;** I did. Thank you guys so much. It's been something that I really want to do for a long time and I'm listening to you all the time so what an honor. Thanks so much you guys.

**CORALINE:&nbsp;** Awesome. Thanks everybody. We'll talk to you next week. Cheers!

**_[Bandwidth for this segment is provided by CacheFly, the world’s fastest CDN. Deliver your content fast with CacheFly. Visit C-A-C-H-E-F-L-Y dot com to learn more.]_**

**_[Would you like to join a conversation with the Rogues and their guests? Want to support the show? We have a forum that allows you to join the conversation and support the show at the same time. You can sign up at RubyRogues.com/Parley.]_**
