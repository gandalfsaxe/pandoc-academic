---
cref: true

# pandoc -F pandoc-crossref -F pandoc-latex-newpage subfig-demo.md -o subfig-demo.pdf
---
  
# Example of two subfig figures
<div id="fig:sbsp">
![The yellow guy with square pants.](spongebob.png){#fig:spongebob width=48%} \hfill
![The dim but loveable pink sea star.](patrick.png){#fig:patrick width=48%}

Two magnificent creatures of the sea.
</div>

Best buddies in [@fig:sbsp]. The protagonist in [@fig:spongebob] and his trusty sidekick in [@fig:patrick].

---

# Example of three subfig figures
<div id="fig:horses">
![Rainbow Dash.](img1.png){#fig:rainbow-dash width=30%} \hfill
![Twilight Sparkle.](img2.png){#fig:twilight-sparkle width=30%} \hfill
![Pinkie Pie.](img3.png){#fig:pinkie-pie width=30%}

Look at my pretty horses!

</div>

We can refer to these fine stallions in several ways:

* **Refer to subfig labels:** Notice the awesome stripes of [@fig:twilight-sparkle], and the bushy tail of [@fig:pinkie-pie] and finally the colorful tail of [@fig:rainbow-dash].
* **Refer to range of labels:** Look at all the pretty horses in subfigures [@fig:twilight-sparkle;@fig:pinkie-pie;@fig:rainbow-dash].
* **Refer to overall figure:** Or simply behold the sight of @fig:horses.