---
layout: page
title: Jung Beta
---

## Unlock the Secrets of Personality with Jung

Jung is a revolutionary API that harnesses the power of advanced language models to uncover the hidden depths of personality and psychological subtext within unstructured text. By providing a block of text where people interact and a secondary directive to guide the analysis, Jung delivers unparalleled insights into the minds and motivations of the individuals mentioned.

## Dive Deep into the Human Psyche

With Jung, you can:

- Uncover key personality traits and characteristics
- Explore the underlying psychological processes, motivations, fears, and desires that drive behavior
- Analyze the subtle dynamics of interpersonal relationships and interactions
- Gain a nuanced understanding of the people behind the words, even when traits aren't explicitly stated

Jung's cutting-edge analysis goes beyond simple trait identification, providing rich distributions over possible trait values. These distributions (specified as both Gaussian with mean and standard deviation and Beta) offer a probabilistic view of each trait, capturing the inherent uncertainty and complexity of human personality.

## Unlock Insights in Everyday Interactions

Jung's powerful analysis can be applied to a wide range of everyday use cases, such as:

- Analyzing interview transcripts and cover letters to gain deeper insights into job candidates' personalities, motivations, soft skills and culture fit.
- Exploring the subtext of instant messaging conversations to better understand potential or current romantic partners
- Identifying potential red flags or concerns in interpersonal communications, such as signs of dishonesty or emotional distress
- Helping law enforcement solve crimes in a less biased, more ethical way
- Maintaining a high standard of care for patients in transition between mental health care providers

Rest assured, Jung does not store any of the data provided for analysis or the results, ensuring the utmost privacy and confidentiality. This makes Jung an ideal solution for mental health applications where patient privacy is of paramount importance.

## API Description

To harness the power of Jung, simply send a POST request to `https://personality-analysis.p.rapidapi.com/jung-{size}` with the following parameters:

- `text` (string): The unstructured text you want to analyze, such as a character description, dialogue transcript, or any text that involves people and their actions.
- `subcommand` (string): An optional secondary directive to refine the analysis towards a specific use case or focus.

Jung will respond with a comprehensive analysis that includes:

- `evidence`: Key excerpts from the text that support the notes and analysis.
- `notes`: A deep dive into the underlying psychological dynamics, motivations, and interpersonal tensions at play.
- `trait_beta`: Probability distributions over likely trait values. Specified as Beta distribution parameters alpha and beta, capturing the nuance and uncertainty of personality.
- `trait_normal`: Summary statistics (mean and standard deviation) for a normal distribution approximating the estimated beta distribution, providing an easily interpretable estimate.

The size options are:

|endpoint|payload limit (kb)|price|
|jung-s|50|$0.125|
|jung-m|150|$0.25|
|jung-l|350|$0.50|
|jung-xl|750|$1.00|

Note that both the text and subcommand count towards this limit.

The majority of these costs are related to inference and RapidAPI margins, you can plan on integrating Jung with confidence as I should be able to bring these costs down by about an order of magnitude within the next 6-9 months.

### RapidAPI

If you haven't used RapidAPI before, you will need to sign up for an account there in order to get headers that are required to make requests. Here are the required headers:

```text
    "X-RapidAPI-Key": "your_rapid_api_key",
    "X-RapidAPI-Host": "personality-analysis.p.rapidapi.com"
```

## Example

Here's an example of how to use the Jung API in Python:

```python
import requests

url = "https://personality-analysis.p.rapidapi.com/jung-s"

payload = {
    "text": "...", # Pretend the text of multiple interviews with Elon Musk is here for brevity.
    "subcommand": "These are transcripts of interviews with Elon Musk.  Your subcommand is to contain your analysis to the person being interviewed and focus your analysis on being maximally informative to someone who might consider working for or having business dealings with him."
}

headers = {
    "X-RapidAPI-Key": "your_rapid_api_key_here",
    "X-RapidAPI-Host": "personality-analysis.p.rapidapi.com"
}

response = requests.request("POST", url, json=payload, headers=headers)

print(response.text)
```

The API will return a response similar to this:

```json
{
  "evidence": {
    "Elon Musk": [
      "Well, I think what is likely to happen, which is really pretty much the way it is, is that something very close to the current lines will be how a ceasefire or truce happens. But you just have a situation right now where whoever goes on the offensive will suffer casualties at several times the rate of whoever's on the defense because you've got defense in depth, you've got minefields, trenches, anti-tank defenses.",
      "I guess if we are able to one day expand to fool the galaxy or whatever, there will be a galactic war at some point.",
      "I suspect that if we are able to go out there and explore other star systems that we\u2026 There's a good chance we find a whole bunch of long dead one planet civilizations that never made it past their home planet.",
      "So really the question is like for every Hamas member that you kill, how many did you create? And if you create more than you killed, you've not succeeded. That's the real situation there.",
      "I mean, look, if I see the slightest indication that there are aliens, I will immediately post on X platform anything I know.",
      "I think we need to understand intelligence, understand consciousness. I mean there are some fundamental questions of what is thought, what is emotion? Is it really just one atom bumping into another atom? It feels like something more than that. So I think we're probably missing some really big things.",
      "I'm generally a proponent of peace. I mean, ignorance is perhaps, in my view, the real enemy to be countered.",
      "Something must stop the cycle of reciprocal violence. Something must stop it, or it'll never stop. Just eye for an eye, tooth for a tooth, limb for a limb, life for a life forever and ever.",
      "I would say that I would be probably left of center on social issues, probably a little bit right of center on economic issues.",
      "Well, our goal is to be as even-handed and fair as possible. Whether someone is right, left, independent, whatever the case may be, that the platform is as fair and as much of a level playing field as possible.",
      "Trust no one, not even yourself. Not trusting yourself.",
      "I mean, I guess you look at somebody's track record over time, and I guess you use your neural net to assess someone.",
      "They're both headed towards AGI. The Tesla approach is much more computer efficient, it had to be. Because we were constrained on this\u2026 We only have 100 watts and [inaudible 02:06:37] computer. 144 trillion operations per second, which sounds like a lot, but is small potatoes these days.",
      "I try to think about, what is going to affect the future in a good way? And holding onto grudges does not affect the future in a good way."
    ]
  },
  "notes": "Elon Musk displays a complex personality shaped by his experiences, relationships, and the immense pressures of his highly public roles. He expresses a general desire for peace and believes ignorance, rather than other humans, is the real enemy. However, he acknowledges the seeming inevitability of conflict, even on a galactic scale if humanity expands beyond Earth.\nMusk advocates for conspicuous acts of kindness to break cycles of violence, as seen in his comments on the Israel-Palestine conflict. He believes whoever escalates will ultimately lose by creating more enemies than they destroy. \nHe is driven by intense curiosity about fundamental questions of consciousness, intelligence and the nature of the universe. There are hints of existential loneliness and a longing for signs we are not alone, as evidenced by his pledge to immediately share any evidence of alien life.\nPolitically, Musk describes himself as left-leaning on social issues and slightly right-leaning economically. He aims for X (Twitter) to be an impartial platform for free speech. However, his outspoken criticism of the \"woke mind virus\" has led to perceptions of conservative alignment.\nTrust seems to be an ongoing struggle, unsurprising given his wealth and fame. Musk half-jokingly says to \"trust no one, not even yourself.\" He relies on evaluating someone's track record over time to decide whether to trust them.\nMusk remains relentlessly optimistic about the potential of AI, seeing a path to AGI through Tesla's efficiency-focused approach born of hardware constraints. However, this optimism may at times blind him to the difficulties and cause him to over-promise on timelines.\nPhilosophically, Musk strives to focus on positively shaping the future rather than holding grudges. His love for his children allows him to see the world with fresh eyes and draws parallels between their cognitive development and the progress of AI. \nOverall, Musk emerges as a visionary futurist with a rare combination of dreamer and engineer. But he is also fallibly human, struggling with the immense social and psychological pressures of his position while doggedly pursuing his ambitious goals for humanity.\n",
  "trait_distributions": {
    "openness": [71.62, 10.419999999999998],
    "conscientiousness": [185.375, 32.79166666666667],
    "extraversion": [31.885416666666664, 37.53124999999999],
    "agreeableness": [50.994791666666664, 65.94270833333333],
    "neuroticism": [57.1125, 73.80416666666666],
    "autonomy": [73.96000000000001, 7.159999999999999],
    "altruism": [21.17825, 14.086749999999999]
  },
  "trait_moments": {
    "openness": { "mean": 0.8300000000000001, "std": 0.12688577540449522 },
    "conscientiousness": { "mean": 0.6599999999999999, "std": 0.18 },
    "extraversion": { "mean": -0.2, "std": 0.21908902300206645 },
    "agreeableness": {
      "mean": -0.12999999999999998,
      "std": 0.17916472867168917
    },
    "neuroticism": { "mean": -0.12999999999999998, "std": 0.2531797780234432 },
    "autonomy": { "mean": 0.9400000000000001, "std": 0.07999999999999999 },
    "altruism": { "mean": 0.2, "std": 0.25298221281347033 }
  }
}
```

Nicely formatted, the data looks like this:

<table><tr><td class="analysis-table">
{% include musk-analysis.html %}
</td></tr></table>

Note that Jung is much more certain about some traits than others in this analysis. I think we can all agree that Elon would score high on openness and autonomy, but his scores for extraversion and altruism are much more questionable, and that is reflected in the estimates.

Because the traits are modeled using a beta distribution, if you perform an analysis on the same person multiple times, you can combine the results in a principled way just by summing the alpha and beta parameters from all the analyses. The estimates from Jung never become stale, only growing more accurate over time as new data comes in.

## Uncover the Depths of Personality

Ready to revolutionize your understanding of the human psyche? Try Jung today and start uncovering the hidden depths of personality in any text. With Jung's cutting-edge analysis and probabilistic trait distributions, you'll gain unparalleled insights into the minds and motivations of the people behind the words.
