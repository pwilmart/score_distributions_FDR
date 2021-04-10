# Score distributions and FDR

How relative sizes of incorrect and correct score distributions affect FDR thresholds.

### Phil Wilmarth
### April 10, 2021

---

![Slide01](images/Slide1.png)

This presentation will explore how separation between incorrect and correct search engine (or classifier function) affects FDR and how the relative sizes of the two distributions affects FDR.

---

![Slide02](images/Slide2.png)

A key concept in most search engine scoring functions is that larger scores are better than small scores, and that the scoring function can separate incorrect matches (low scores) from correct matches (higher scores). More separation between incorrect and correct distributions is more better. Combinations of scores and other information often improves score distributions. These classifier functions take many forms and can be static (think PeptideProphet) or dynamic (think Percolator). False discovery rate calculations involve tail integrations, so distribution shapes without long tails are better (particularly the right-hand tail of the incorrect scores).

---

![Slide03](images/Slide3.png)

Peptide identification methods in shotgun proteomics usually involve matching MS2 spectra to theoretical peptide sequences (database searching). We end up with a mixture of correct matches and incorrect matches. We use score threshold cutoffs to decide which (putative) correct peptides we map back to proteins. If the incorrect score distribution (in red) sits at the same x-axis location as the correct score distribution (in blue), we are dead in the water. No x-axis cutoff can give us mostly blue matches by excluding the red matches. This search engine would not be very popular.

---

![Slide04](images/Slide4.png)

This scoring function was chosen wisely because it is the Holy Grail of proteomics. If we can have complete separation between the score distributions, we do not need target/decoy strategies because the FDR is always perfect (zero). If only life were like this. Proteomics data is a mixed bag of ions. We have peptides in sizes and charges that we can sequence. And we have so much else. Some ions are not peptides. Some peptides do not fragment well. Some peptides are modified or otherwise not included in our theoretical peptide space. Some peptides are low abundance and noisy. There are many reasons why we do not have great scores for all peptides.

---

![Slide05](images/Slide5.png)

We usually have incorrect and correct distributions that are partially resolved and overlap like we see here. This is why we talk about false discovery rates. When we have overlapping distributions, we want to find a search score value on the x-axis that captures most of the correct matches with higher scores while simultaneously excluding most of the incorrect matches with lower scores. We are integrating the right-hand tail of the incorrect distribution and trying to have it be some desired fraction of the area under the correct score distribution. Here we show the common 1% FDR situation. We recover a large fraction of the blue distribution, but we do not get all the possible correct matches. The factors that affect how much of the blue curve we can recover are: how well separated the two distributions are, the shape of the incorrect score distribution’s tail, and the relative areas under the two distributions. The last factor is under appreciated.

---

![Slide06](images/Slide6.png)

We will create two Gaussian distributions located so that the distributions overlap. We will keep the location and shapes of the distributions the same. We will only vary their relative areas. We will determine the 1% FDR cutoff and compute how much of the correct distribution we can recover. We will step though 20 iterations from 10:1 to 1:10.

---

![Slide07](images/Slide7.png)

When the correct distribution is small, the tail of the larger incorrect distribution is a big deal. The recovery is pretty low.

---

![Slide08](images/Slide8.png)


---

![Slide09](images/Slide9.png)


---

![Slide10](images/Slide10.png)


---

![Slide11](images/Slide11.png)


---

![Slide12](images/Slide12.png)

We have half as large an incorrect distribution as in the 10:1 case and we are starting to see some improvement in the recovery.

---

![Slide13](images/Slide13.png)


---

![Slide14](images/Slide14.png)


---

![Slide15](images/Slide15.png)

At a 2:1 ratio, we have improved recovery from half to three quarters.

---

![Slide16](images/Slide16.png)


---

![Slide17](images/Slide17.png)


---

![Slide18](images/Slide18.png)


---

![Slide19](images/Slide19.png)


---

![Slide20](images/Slide20.png)


---

![Slide21](images/Slide21.png)

At a 1:2 ratio, we are seeing less and less contribution from the incorrect tail and the recovery is getting closer to 100%.

---

![Slide22](images/Slide22.png)


---

![Slide23](images/Slide23.png)


---

![Slide24](images/Slide24.png)


---

![Slide25](images/Slide25.png)

Not surprisingly, when the incorrect distribution is small, we can lower the score cutoff and recover nearly all the correct matches.

---

![Slide26](images/Slide26.png)

We kept the same two distributions in the same locations and determined the correct recovery at the same 1% FDR. We only changed the relative areas of the two distributions. The areas of these distributions in practice are the numbers of incorrect and correct PSMs in our experiment. If we want to recovery more correct PSMs (increase sensitivity), one way is to decrease the number of incorrect matches (the noise).

---

![Slide27](images/Slide27.png)

In the early days of proteomics, fixed score cutoffs were common. This had issues. We need to adjust score cutoffs to maintain constant FDR if the relative sizes of the correct or incorrect distributions change. Adaptive classifiers like Percolator are mostly adapting to the distribution relative size changes. The inherent features associated with correct or incorrect peptides do not change much between experiments in most cases.

---

![Slide28](images/Slide28.png)

The order of logical operations in proteomics data analysis matter a lot. A good example these days is accurate mass. Instruments can measure charge-to-mass ratios with great precision. We could filter PSMs by search score first and then do further filtering by the mass differences between the measured ion and its assigned sequence. That reduces sensitivity because the score distributions overlap and we do not have optimal recovery. If we check the mass differences first, we can reduce the incorrect score distribution size and increase the recovery of correct peptides.

Alternative strategies try to explicitly incorporate peptide categories into classifier functions. That can look attractive on paper but be challenging in practice.

---

Finished.
