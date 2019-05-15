---
title: advice to my friends
subtitle: my advice to my friends who are trying to get internships for the summer
date: May 15, 2019
---

I always have friends asking me what my advice is to land internships for the summer and I always give them a few helpful tips but I never really get time to tell them everything. So I am writing this post to centralize my thoughts so that I can share everything in one go.

So here are my (extremely disorganized) set of tips to anyone looking for an internship!

## Apply Early

Not like December early, or October early. I mean start looking during the summer itself. Ideally you should be looking for your next internship while at your current one (if you have one).  Now this doesn't mean you should be disrespectful and look at job postings while you're at work, but the general point is that you should be looking in July or August.

You honestly wont find my posts BUT these are generally the posts where recruiters will actually look at your resume. Once it gets to December, they will have thousands of resume's and will just give up. However, you shouldn't stop applying after September, but chances do start decreasing after that (except for big companies).

## Apply to Companies that DON'T post on LinkedIn/GlassDoor

If you are like everyone else, you'll probably be scouring LinkedIn, GlassDoor, and all of these other job marketplaces. While thats fine, you have thousands of other students doing the same thing. Instead think of some companies that are sort of niche but you would like to work at, and try to apply or email that company. Most people ignore this but it really does work; my upcoming internship was not on any job forums (as far as I know), so the applicant pool was much much smaller.

## Coding Tests

The first step towards landing your internship is usually a coding test. These vary in difficulty from a simple parenthesis question to an extremely complex math and recursive function. You should do the usual HackerRank and LeetCode stuff. The only way to really get good at these are to do a lot of them.

However I do have on trick to coming up with solutions to a lot of coding challenges. The trick is to do the program by hand on paper first. Chances are your brain will come up with an efficient algorithm to solve it off the bat. For example, there is a security guards problem where you have a grid that contains guards who can look up, down, left, and right but not diagonally. You are given a point on the grid and you have to say whether or not that block is hidden from the guards as efficiently as possible. Now you can do this with just some for loops stacked inside of each other, but there is a more optimal solution. I was able to find something that was pretty efficient by just drawing the grid on paper, filling in the guard position with one of the test cases they gave, and tried to figure out if the spot was safe by hand. Whatever strategy my brain came up with was more efficient than just doing the naive solution. Try it yourself, I'm sure you will figure it out quickly. Now this is a really really simple problem but this trick really does work on some of the most complex questions I have gotten in the past.

**Even if you complete the test and ace all of the test cases, you still have a 75% chance of not even hearing back.** That's just how it is, so don't be discouraged if you don't hear back. However, it doesn't hurt to follow up with your recruiter once or twice at max.

## Interview Advice

I have a lot of advice for both technical interviews and "phone screens" or whatever else they call non-technical interviews. This is pretty much your last step before you get an offer BUT messing up at any of these will ruin your chances. I'd highly recommend following some of the tips below since they seemed to have worked for me.

### Phone Screens

These are pretty important to nail. They will determine if you will even get a technical interview. My best advice is to have some pre-written answers to simple questions such as "what is your greatest strength/weakness" and "what is your favorite project and why". Additionally, when you are on the phone, have your resume open so you can be consistent with your answers and point the recruiter to relevant parts of your resume as you answer their questions.

At the end, always ask something along the lines of "If you decide to move forward, what are some of the next steps I can expect?" This will somewhat force the recruiter to decide on the spot if they like you or not, and you will almost always get a "Let's schedule a technical interview" response or a "You will have 2 technical interviews, I will email you a follow-up." If they don't like you or need time they will probably say something like "I'll email you the next steps if we decide to move forward" in which case it's usually 50-50 if they liked you or not.

### Live Coding Challenges

Honestly, I don't have much advice here. They are very stressful and hard and you just have to do your best to work through the problem. Make sure you talk about what you are doing every few minutes, because if you are just silent the whole time, the interviewer will get bored. Other than that, use the same advice from the "Coding Tests" section.

Also make sure you say what your strategy is going to be before you start coding. If you understood the problem wrong or missed something, they will usually tell you so you don't sit and program something incorrect for an hour. Also **always, always, always** say what the naive solution is and why it's bad before you give your solution. That shows that you understand that there is a slow way to do it, but they should hire you because you are easily able to optimize it. **THERE IS ALWAYS A BETTER SOLUTION THAN THE FIRST THING THAT COMES TO MIND** The point of the coding tests are to have a very obvious naive solution and a hidden efficient solution, so if you can't come up with a second solution, just say something like "I know the naive solution but I am struggling to figure out the optimized one," and they will more than likely help you.

It is always nice when you do something the interviewer doesn't know (syntax wise) such as object destructuring (assuming they aren't experts in your language), so try to find one or two neat tricks. If you teach the interviewer something along the way, they will actually be interested in what you have to say and there will be some credibility behind your work. However, don't just do one-liners for complex functions.

#### Code Quality

**THIS IS FUCKING IMPORTANT**

This really fucking pisses me off... Take a look at this code:

```js
const api = (name, apiKey) => {
  if (apiKey) {
    if (isValid(apiKey)) {
      if (name) {
        if (name.length < 25) {
          // we know that all of these conditions are true
        } else {
          throw new Error('that is a long ass name');
        }
      } else {
        throw new Error('missing name');
      }
    } else {
      throw new Error('api key is not valid');
    }
  } else {
    throw new Error('missing api key');
  }
}
```

Why? Why? WHYYYY???

No one wants to read that. If I see that code anywhere, I honestly just stop reading, and so will pretty much every other interviewer.

Please use "return first" programming. That code is the equivalent to the following code, but the following code is so much more readable.

```js
const api = (name, apiKey) => {
  if (!apiKey) {
    throw new Error('missing api key');
  }
  if (!isValid(apiKey)) {
    throw new Error('api key is not valid');
  }
  if (!name) {
    throw new Error('missing name');
  }
  if (name.length > 25) {
    throw new Error('that is a long ass name');
  }
  // we know that all of these conditions are true
}
```

Not only is this less code, it is also much easier to read. As I go from top to bottom, I can see what the conditions are. The `apiKey` has to exist and be valid, and `name` has to exist and be less than 25 characters long. I can read that in one go, whereas the shitty code above is hard to follow. You can barely tell which `else` goes to which `if`. You may also be tempted to use `else if` and there isn't anything wrong with it, but its just better if you `throw` or `return` instead. There are overall less characters to read.

**If you have nested `if`s, most of the time you are doing something wrong.** I very rarely have a nested `if` or even `else` blocks. If you see that you have a lot of these, break it out into other functions or clean up your logic.

Interviewers are especially looking for this kind of code to see if you are hireable. The last thing they want is unreadable code in their codebase.

## Conclusion

I'll continually update this post with more advice as I think of it or gain more experience or inside information. I really hope that this helped you in some way and if you have any suggestions, feel free to email me!
