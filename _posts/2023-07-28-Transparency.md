---
layout: post
title: "Who's Paying Our Pollies?"
date: 2023-07-28
categories: 
---

Each year, the Australian Electorial Commission requires political parties and other political entities to declare who they've received money from (above a certain threshold) and this information is publishes on the AEC's Transparency Register.

Whilst there are certain issues with the implementation (for example, the public can only read this information after the financial year is over), the Transparency Register is a good idea in principle. It is, however, only effective if people take the time to actually look at the data.

So I decided to take a gander. There were a few interesting discoveries about the 21/22 data that Iwant to write about. A general overview can be found in the following Tableau dashboard:

(dashboard)

(information on donations and the amount of public funding received)

## The absurdity of Mineralogy

The first thing that stands out is the sheer amount of money that Clive Palmer has donated to himself. More precisely, the money that Clive Palmer's company Mineralogy Pty Ltd has donated to Clive Palmer's United Australia Party. 

Consider the following distribution of donations where we exclude those made by Mineralogy:

PIC

The median donation amount is about $5000, but there are some significant donations; the mean donation is about $15,000. The largest donation is $1.5 million. Now, look at what happens if we include Mineralogy, whose donations have been labelled in orange:

PIC
 
You can barely even see the measly 1.5 million dollar donation! The largest donation is now $50 million and the average donation has moved from $15,000 to $60,000. In fact, this single donor accounts for three quarters of all money donated, and it's all going to one party:

PIC
 
We could spend a while discussing the problematic aspects of this. For now I will just mention the impact it has on the statistical analysis; Mineralogy Pty Ltd is certainly an outlier and is likely to skew a lot of the results. 

## The (other) top donors
It's not only important to know who the top donors are, but also who they're donating to. Let's consider the two major parties, the Australian Labor Party and the Liberal Party. Indeed, 71% of donations were made to one of these parties. A more precise breakdown is as follows:

PIC
 
Of the 71% of people who donated to either Labor or Liberal, almost half actually donated to both. This suggests that these donors aren't donating just because they are Labor or Liberal supporters.

The largest donor for both Labor and Liberal was the same; non-other than Australia's third richest person, Andrew Pratt. Pratt, the executive chairman of recycling company Visy and Pratt Industries, which is the worlds largest privately owned packaging and paper company, donated $1.67 million to the Liberal party and $1.96 million to the Labor party. These were the largest donations for both of these parties, but the amount isn't much for a man who's net worth is about $25 billion.

PIC

It can be difficult to figure out what some of these companies are: Sugolena Holdings, for example, doesn't have a website or Wikipedia entry. If you Google it, all you find are articles about the large donations they've made to the Liberal party. It is appears to be the corporation behind the property empire built by reclusive Isaac and the late Susan Wakil. The couple initially gained their fortune in the clothing industry before investing in property. They are very philanthropic, donating large amounts of money to charity.

Oryxium Investments is part of the Lowy family's business empire, but it is also difficult to find specific information about it. This is because the company seems to have been created for the explicit purpose of making large donations to the Liberal party. Indeed, it has no website, address, or even employees.

Overall, it seems that if you want to know who is really making these large donations to the Liberal party you're going to need to do a lot of digging.

The Labor party's donor portfolio is a little different: three of the five are from unions or other organisations representing industry workers. This is not without it's problems: there are plenty of examples of unions putting pressure on politicians to make decisions that adversely affect the rest of the population. Indeed, one example might be the Pharmacy Guilds staunch opposition to the recently proposed changed to prescriptions. These problems, however, fit into the wider problem of any large donor having unfair access to or influence on politicians. It's at least clear who is making these donations, which can't be said of the mysterious corporate donations. The transparency register becomes significantly less transparent if the donors themselves are opaque.

## "Other receipts"

In the transparency register, not only do we see the donations made to the political parties, we also see what other money the parties have received. These are found in the "detailed receipts". A receipt can be either be from a donation made, a subscription payment, or an 'other receipts'. Earlier years also have receipts from public funding and 'unspecified', but it seems that this is not longer reported in this data.

Let's take a look at the different types of receipts for the 2021-2022 financial year. We've removed Mineralogy Pty Ltd so as not to skew the values. By number of receipts, 'other receipts' make up almost three quarters of all the receipts:

PIC
 
Only a tiny slither of the receipts are subscription payments, and almost a quarter are from donations. The picture is even starker if we look at the total value of the receipts:

PIC
 
Other receipts make up about $530 million; about 87% of the total receipts.

What counts as 'other receipts'? According to the government, "other receipts are any amounts received other than donations, including income from sales of goods or services, interest on bank accounts, and public funding." Moreover, "for amounts that are received above the disclosure threshold, returns must disclose the full name and address of the donor, the amount received, and whether the receipt is a 'donation' or 'other receipt'."

So the receipts are basically broken down into 'donations' and 'everything else' (with a small amount of subscriptions). Not only this, it seems that a party can essentially choose whether an amount it receives counts as a donation or other receipt. This also explains why public funding is no longer it's own category; it has been lumped into 'other'.

The fact is, we have no idea what a given 'other receipt' is. We likely can't even say that it wasn't a donation. We know that the parties received $530 million and we know who they received the money from, but we don't know what the money is for.

## Receipt discrepancies

Continuing on from the previous section, we can compare the 'donations made' table with the 'detailed receipts' table to see cases where a political party has received more money from a donor 

One example is that Morgans Financial Ltd, a stockbroking company, donated $13,500 to the Queensland division of the Labor Party. However, the Labor party declared $79,000 worth of receipts from Morgans. In this case, the discrepancy is clear; probably it was some kind of return on investments.

Another example is Spirits & Cocktails Australia, which is the peak body for spirits manufacturing in Australia. They donated only $1,418 but the Labor Party in Queensland received $12,000 from them in total. In another case, an individual, Robert Gunning, donated $8000 to the Liberal party in Queensland, but they received a total of $18,485 from him. This all begs the question of what these other receipts are for.

Even more curious is the case where the value of the donations exceed the amount that the party has claimed to have received. There are many examples of this. For example, the Pharmacy Guild of Australia donated $47,330 to the Labor party in Queensland, who reported only $2000 of receipts from them.  It's likely that I'm just not knowledgeable enough to explain such cases; perhaps the $2000 is a net value, so payments to the Pharmacy Guild are subtracted from the donation value.

Certainly not all of these examples have devious underpinnings. The issue is that we have no way of knowing.

## Maybe we can do better but who am I to say

It is generally accepted that the reporting and disclosing of political donations is a good idea if you want to ensure that political parties aren't being unduly influenced by other parties. 

I've identified two possible issues with the transparency registry. The first is that when the donation is made via a corporation, it can be very difficult to work out who is doing the donating. This is not a problem unique to this situation; in everyday life it is difficult to find out which companies own which other companies and so on. The second is that a vast majority of the money received by political parties is filed under 'other receipts' and so we have no idea what the purpose of this money is. Maybe this could be fixed by having finer categories for receipts.

An issue with our current register that I haven't mentioned is that information is only released 'after the fact'. The public can find out who the political parties have received money from, but up to a year after they've received the money. This means that, during an election for example, the public won't be aware of large political donations until after they've voted. A more frequently updated register would give more timely information to the public and provide more pressure on political parties to be open about their finances. One can even go beyond a frequently updated register: the Czech Republic, for example, allows the public to view all the transactions of the bank accounts to which donations must be deposited.

Let's face it though: it is extremely difficult to create robust political finance regulations. There are multiple factors to this, as described in an EU report on political financing in the EU. For one, there are political difficulties. For example, the public will often be opposed to increasing public funding to political parties, even though it can be an effective method of reducing a parties reliance on corporate donations (and hence their influence on politics). Secondly, there are strong incentives for political parties to try to circumvent the laws or find loopholes. When strict regulations on political financing was introduced in the UK in 2000, parties began reporting significantly more 'loans', many of which were believed to be donations in disguise. A lot of energy can be expended by a government trying to oversee and regulate political financing.
All this to say that political finance is complicated and there are no easy solutions. Certainly I'm not qualified to offer any.

