---
layout: post
title: Introducing Jung, your AI powered personality analyst!
---

Hello. I'm happy to announce the beta launch of my personality profiling and analysis tool, Jung! Jung can take unstructured text and a contextual directive and help you peer into the depths of someone's psyche, extracting personality traits, subtext and hidden motivators. If you'd like to know the details of the Jung API, head over to the [API page](./jung/). For now, I'd like to focus on some fun demonstrations to give you a sense of Jung's abilities.

Given that those of us in the United States are in an election year and politics are delicious clickbait (sorry, not sorry), I thought I'd start with a comparison of the two men vying for the job of our fearless leader. That's right, we're going to dive into the minds of Donald Trump and Joe Biden to try and see how Jung could help a prospective voter who was undecided (do they still exist?) pick the best candidate.

To perform this analysis, I started by collecting and bundling together text from multiple recent interviews to fill up my available context, so Jung would have plenty to work with. If you'd like to replicate this analysis you can go to the [presidential project](https://www.presidency.ucsb.edu/presidents) and select the three most recent interviews for each president.

In addition to taking text to analyze, Jung takes a subcommand that helps guide its analysis. Here is the subcommand used for these analyses:

```text
These are transcripts of interviews with a presidential candate.  Your subcommand is to contain your analysis to the person being interviewed and focus your analysis on being maximally informative to a potential voter who was undecided and wanted to get a deep understanding of what kind of person the interviewee is.  Try to avoid being biased by preexisting knowledge of the subject and focus on the provided text.
```

I want to preface this analysis by noting that I've made many attempts to control for ideological, social, racial and other biases in Jung. Jung considers issues from diverse perspectives (including both conservative and liberal) and you can see from the subcommand that it has been instructed to avoid being biased by prior knowledge. To put in it plain English - I did my best to give Donny a fair analysis without compromising the objectivity of the analytical process.

With that out of the way, let's dive into the output of Jung. I've placed Biden and Trump side by side for easy comparison:

<table>
    <tr>
        <td class="analysis-table" style="background-color: rgb(0, 0, 48)">
        {% include biden-analysis.html %}
        </td>
        <td class="analysis-table" style="background-color: rgb(48, 0, 0)">
        {% include trump-analysis.html %}
        </td>
    </tr>
</table>

Not too shabby! Jung clocks both Biden and Trump well, which isn't that useful in this case since I think everyone knows what each of the candidates are about, but it could be very useful in other circumstances such as hiring, medical support systems, criminal justice and so forth where a decision maker might lack sufficient time to make a nuanced decision considering all the evidence. With Jung's help, you can quickly gain psychological insights from large volumes of conversational text.

Note that the traits listed here are the [Big 5](https://en.wikipedia.org/wiki/Big_Five_personality_traits), with the addition of autonomy and altruism which are not adequately captured by the Big 5. Here are the definitions for reference:

- Autonomy: the individual's independence, self-determination, and willingness to make decisions based on personal judgment. Autonomous individuals are skeptical of authority and do not care about external expectations.
- Altruism: the individual's concern for the well-being of others, willingness to help, and tendency to prioritize the needs of others over their own. Altruistic individuals are generous, compassionate and selflessness in their actions and decisions.

You might also notice the red line on the charts doesn't exactly line up with the listed mean. This is because the mean and standard deviation are from a gaussian approximation, the true underlying distribution is beta, and the charts are using the mode, which is more meaningful for beta distrbutions with skew than the average. The guassian mean and deviation are provided because they're easier to conceptualize but the beta distributions are correct.  Working with beta distributions also has the nice property that if you have Jung analyze someone more than once, you can combine the results in a principled way just by summing the alpha and beta parameters for each trait.

Those of you with a background in psychometrics might be used to seeing traits on a 1-10 or 1-100 scale, and wonder why the traits are expressed in the [-1, 1] range. This is because centering the neutral value at 0 reduces scale bias caused by human (and, by extension, LLM) evaluation resulting from the skewed distributions of graded schoolwork and product reviews.

If you enjoyed this, stay tuned because I plan to run a whole series of interesting comparisons in the near future.
