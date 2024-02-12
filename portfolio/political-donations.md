---
layout: post
title: "Who's Paying Our Pollies? A Peak Into the Transparency Register"
date: 2023-07-28
permalink: '/portfolio/political-donations'
---

Each year, political parties and other political entities are required to declare who they've received money from (above a certain threshold) to the Australian Electoral Commission and this information is published on the AEC's [Transparency Register](https://transparency.aec.gov.au/).

Whilst there are certain issues with the implementation (for example, the public can only read this information after the financial year is over), the transparency register gives the Australian public the chance to see who their politicians are accepting money from and whether this might impact their actions.
The register is, however, only effective if people take the time to actually look at the data.

So I decided to take a gander. 
There were a few interesting discoveries about the 21/22 data that I want to write about. 
I summarised my findings in the following [Tableau dashboard](https://public.tableau.com/views/PoliticalDonationsinAustraliawebpageversion/Dashboard?:language=en-US&:display_count=n&:origin=viz_share_link):


<div 
    class='tableauPlaceholder' 
    id='viz1690817918520' 
    style='width:100%; margin:auto;'
>
<noscript>
<a href='#'><img alt='POLITICAL DONATIONS IN AUSTRALIA  ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Po&#47;PoliticalDonationsinAustraliawebpageversion&#47;Dashboard&#47;1_rss.png' style='border: none' /></a>
</noscript>
<object class='tableauViz'  style='display:none;'>
<param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' />
<param name='embed_code_version' value='3' />
<param name='site_root' value='' />
<param name='name' value='PoliticalDonationsinAustraliawebpageversion&#47;Dashboard' />
<param name='tabs' value='no' />
<param name='toolbar' value='yes' />
<param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Po&#47;PoliticalDonationsinAustraliawebpageversion&#47;Dashboard&#47;1.png' />
<param name='animate_transition' value='yes' />
<param name='display_static_image' value='yes' />
<param name='display_spinner' value='yes' />
<param name='display_overlay' value='yes' />
<param name='display_count' value='yes' />
<param name='language' value='en-US' />
</object>
</div>                

<script type='text/javascript'>
    var divElement = document.getElementById('viz1690817918520');
    var vizElement = divElement.getElementsByTagName('object')[0];
    if ( divElement.offsetWidth > 800 ) {
        vizElement.style.width='650px';
        vizElement.style.height='887px';
    } else if ( divElement.offsetWidth > 500 ) { 
        vizElement.style.width='650px';
        vizElement.style.height='887px';
    } else { 
        vizElement.style.width='100%';
        vizElement.style.height='1727px';
    }                     
    var scriptElement = document.createElement('script');
    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';
    vizElement.parentNode.insertBefore(scriptElement, vizElement);
</script>

<br>

## The absurdity of Mineralogy

The first thing that stands out is the sheer amount of money that mining mogul Clive Palmer has donated to himself. 
More precisely, the money that Clive Palmer's company Mineralogy Pty Ltd has donated to Clive Palmer's United Australia Party. 

Consider the following distribution of donations made by everyone except Mineralogy Pty Ltd: 

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/donations-wo-mineralogy.png"
  style="width:90%"
  >
  <figcaption>
    Distribution of donations in the 20/21 financial year, not including Mineralogy Pty Ltd
  </figcaption>
</figure>
</center>

The median donation amount is about $5000, but there are some significant donations; the mean donation is about $15,000. The largest donation is $1.5 million. Now, look at what happens if we include Mineralogy, whose donations have been labelled in orange:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/donations-w-mineralogy.png"
  style="width:90%"
  >
  <figcaption>
    Distribution of donations, including Mineralogy Pty Ltd
  </figcaption>
</figure>
</center>
 
You can barely even see the measly 1.5 million dollar donation! The largest donation is now $50 million and the average donation has moved from $15,000 to $60,000. In fact, this single donor accounts for three-quarters of all money donated, and it's all going to one party:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/mineralogy-pie.png"
  >
  <figcaption>
    The proportion of money donated by Mineralogy Pty Ltd
  </figcaption>
</figure>
</center>
 
Certainly, this raises questions about the potential of extremely wealthy people funding their own political parties to influence politics in any way they see fit.
For now, I'll just mention the impact it has on the data; Mineralogy Pty Ltd is certainly an outlier and we'll have to remove it when calculating certain statistics to get a clear picture of what the rest of the donations look like.

## The (other) top donors
It's not only important to know who the top donors are, but also to who they're donating to. Let's consider the two major parties, the Australian Labor Party and the Liberal Party. Indeed, 71% of donations were made to one of these parties, with a more precise breakdown as follows:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/donor-share-pie.png"
  >
  <figcaption>
    Breakdown of donors based on if they donated to Labor or Liberal
  </figcaption>
</figure>
</center>

Of the 71% of people who donated to either Labor or Liberal, almost half actually donated to both. 
It seems these donors aren't donating simply because they're Labor or Liberal supporters.

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/pratt.jpg"
  style="width:50%"
  >
  <figcaption>
    Andrew Pratt, Labor and Liberal's biggest donor
  </figcaption>
</figure>
</center>

The largest donor for both Labor and Liberal was the same; non-other than Australia's third-richest person, Andrew Pratt. Pratt, the executive chairman of recycling company Visy and Pratt Industries, which is the world's largest privately owned packaging and paper company, donated $1.67 million to the Liberal Party and $1.96 million to the Labor party. These were the largest donations for both of these parties, but the amount isn't much for a man whose net worth is about $25 billion.

Here are the remaining top donors for the Liberal and Labor parties:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/top-liberal-donors.png"
  style="width:80%"
  >
  <figcaption>
    Top five Liberal Party donors
  </figcaption>
</figure>
</center>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/top-labor-donors.png"
  style="width:80%"
  >
  <figcaption>
    Top five Labor Party donors
  </figcaption>
</figure>
</center>


It can be difficult to figure out what some of these companies are: Sugolena Holdings, for example, doesn't have a website or Wikipedia entry. If you Google it, all you find are articles about the large donations they've made to the Liberal Party. It appears to be the corporation behind the property empire built by Isaac Wakil and the late Susan Wakil. 
The couple initially gained their fortune in the clothing industry before investing in property. 
They're known to be very philanthropic, contributing large amounts of money to health, education, and the arts.

Oryxium Investments is part of the Lowy family's business empire, but it is also difficult to find specific information about it. This is because the company seems to have been created for the [explicit purpose of making large donations to the Liberal Party](https://independentaustralia.net/politics/politics-display/lowy-family-use-loophole-to-donate-550000-to-liberal-party,17340). Indeed, it has no website, address, or even employees.

Overall, it seems that if you want to know who is really making these large donations to the Liberal Party you're going to need to do a lot of digging.

The Labor party's donor portfolio is rather different: three of the five are from unions or other organisations representing industry workers. 
This is not without its problems: there are plenty of examples of unions putting pressure on politicians to make decisions that adversely affect the rest of the population.
Indeed, one example might be the Pharmacy Guilds [staunch opposition](https://www.abc.net.au/news/2023-05-09/pharmacy-guild-pbs-robocalls-distress-medication-users/102322136) to the recently proposed changed to the distribution of prescription medication.

The wider problem of large donors having unfair access to or influence on politicians exists for all donors.
At least when the donor is a union it is clear who is making the donations, which can't be said of the mysterious corporate donors. 
The transparency register becomes somewhat less transparent when the donors themselves are opaque.

## "Other receipts"

The transparency register not only shows the donations made to each political party; it also shows what other money the parties have received. 
These are found in the "detailed receipts" table.
A receipt can be either from a donation made, a subscription payment, or an 'other receipts'. 
Earlier years also had receipts from public funding and 'unspecified', but these are either no longer reported or a part of the 'other'.

Let's take a look at the different types of receipts for the 2021-2022 financial year.
We've removed Mineralogy Pty Ltd so as not to skew the values.
By number of receipts, 'other receipts' make up almost three-quarters of all the receipts:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/other-receipts-amount.png"
  >
  <figcaption>
    Almost a quarter of receipts are classified as 'other'
  </figcaption>
</figure>
</center>
 
Only a tiny slither of the receipts are subscription payments, and almost a quarter are from donations.
The picture is even starker if we look at the total value of the receipts:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/transparency/other-receipts-value.png"
  >
  <figcaption>
    87% of the money received by political parties is filed under 'other receipts'
  </figcaption>
</figure>
</center>
 
Other receipts make up about $530 million; about 87% of the total receipts.

What counts as 'other receipts'? According to [the government](https://www.aph.gov.au/About_Parliament/Parliamentary_departments/Parliamentary_Library/pubs/rp/rp2122/Quick_Guides/ElectionFundingStates#_ftn2), "other receipts are any amounts received other than donations, including income from sales of goods or services, interest on bank accounts, and public funding." 
Moreover, "for amounts that are received above the disclosure threshold, returns must disclose the full name and address of the donor, the amount received, and whether the receipt is a 'donation' or 'other receipt'."

So the receipts are basically broken down into 'donations' and 'everything else' (with a small amount of subscriptions).
It also seems that a party likely get to choose whether an amount it receives counts as a donation or other receipt.
This also explains why public funding is no longer its own category; it has been lumped into 'other'.

The fact is, we don't know what a given 'other receipt' is.
We can't even say that it wasn't a donation.
We know that the parties received $530 million and we know who they received the money from, but we don't know what the money is for.

## Receipt discrepancies

Continuing on from the previous section, we can compare the 'donations made' table with the 'detailed receipts' table to see cases where a party has received money from a donor beyond donations.
One could also look directly at the 'other receipts', but I wanted to see if there were any discrepancies.

One example is that Morgans Financial Ltd, a stockbroking company, donated $13,500 to the Queensland division of the Labor Party.
However, the Labor party declared $79,000 worth of receipts from Morgans.
This case is reasonably clear; probably it was some kind of return on investments.

Another example is Spirits & Cocktails Australia, which is the peak body for spirits manufacturing in Australia.
They donated only $1,418 but the Labor Party in Queensland received $12,000 from them in total.
In another case, an individual, Robert Gunning, donated $8000 to the Liberal Party in Queensland, but they received a total of $18,485 from him.
What are these receipts for?

Even more curious is the case where the value of the donations exceeds the amount that the party has claimed to have received.
There are many examples of this.
For example, the Pharmacy Guild of Australia donated $47,330 to the Labor party in Queensland, which reported only $2000 of receipts from them.
Probably I'm just not knowledgeable enough to explain such cases; maybe the $2000 is a net value, so payments to the Pharmacy Guild are subtracted from the donation value.

Certainly not all of these examples have devious underpinnings, but I am curious about the purpose of these receipts.

## Maybe we can do better but who am I to say

It is generally accepted that the reporting and disclosing of political donations is a good idea if you want to ensure that political parties aren't being unduly influenced by other parties. 

I found two possible issues with the transparency registry.
The first is that when the donation is made via a corporation, it can be very difficult to work out who is the one donating.
This is not a problem unique to this situation; in everyday life, it is difficult to find out which companies own which other companies and so on.
The second is that a vast majority of the money received by political parties is filed under 'other receipts' and so we have no idea what the purpose of this money is.
Maybe this could be fixed by having finer categories for receipts.

An issue with our current register that I haven't discussed is that information is only released 'after the fact'.
The public can find out who the political parties have received money from, but only at the end of the year.
This means that, during an election for example, the public won't know of any large political donations until after they've voted.
A more frequently updated register would give more timely information to the public and provide more pressure on political parties to be open about their finances.
One can even go beyond a frequently updated register: the Czech Republic, for example, allows the public to view all the transactions of the bank accounts to which donations must be deposited.

Let's face it though: it's extremely difficult to create robust political finance regulations.
There are multiple factors to this, as described in an [EU report](https://www.europarl.europa.eu/RegData/etudes/STUD/2021/694836/IPOL_STU(2021)694836_EN.pdf) on political financing in the EU.
For one, there are political difficulties; for example, the public will often oppose increasing public funding to political parties, even though it can be an effective method of reducing a party's reliance on corporate donations (and hence their influence on politics).
Secondly, there are strong incentives for political parties to try to circumvent the laws or find loopholes.
When strict regulations on political financing were introduced in the UK in 2000, parties began reporting significantly more 'loans', many of which were believed to be donations in disguise.
A lot of energy can be expended by a government trying to oversee and regulate political financing.

All this to say that political finance is complicated and there are no easy solutions.
I've enjoyed learning about it nonetheless.

