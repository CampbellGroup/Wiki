# Electron Configuration

Orbital angular momenta are abbreviated as follows (abbreviation, $l$): (S, 0), (P, 1), ( D, 2), (F, 3), (G, 4). For a given total angular orbital momentum $l$, the orbital angular momentum may take any of the $(2l+1)$ integer values from $-l$ to $l$. The Pauli exclusion principle restricts these $(2l+1)$ angular momenta levels to each be occupied by at most 2 electrons. This means that with 2 electrons and $(2l+1)$ angular momenta values, an atomic sub-shell (defined by *l*) can have up to $2\times2(l+1)=(4l+2)$ electrons.

| Sub-Shell | $l$ | Maximum Number of Electrons |
| :--------: | :-: | :----------------------:  |
| S | 0 | 2 |
| P | 1 | 6 |
| D | 2 | 10 |
| F | 3 | 14 |
| G | 4 | 18 |

The sub-shells make up atomic shells that give us the overall electron configuration. These shells are defined by the maximum sub-shell that it contains. For example, the first S sub-shell to fill up is the 1s sub shell, which forms the shell K. The shells are given here as (Shell name, maximum sub-shell): (K, 1S), (L, 2P), (M, 3D), (N, 4F), (O, 5G). Each shell contains all sub-shells of *l* lower than the maximum sub-shell. For example, shell M contains the 3D, 3P, and 3S sub-shells, where the "3'' is an indication that these sub-shells come from the third (M) shell. Because of this redundancy, we often only refer to shells using the number prefacing the sub-shell as opposed to the actual letter for the shell (which is sometimes used more commonly in other fields). As each shell contains preceding sub-shells, the $n^{th}$ shell may hold up to $\sum_{l=0}^{n-1}(4l+2)=2n^2$ electrons. The summation is from the first sub shell of *l* = 0 to to the $n^{th}$ sub-shell with $l=n-1$.

| Sub-Shell | Sub-Shell Max Number of Electrons | Shell Max Number of Electrons |
| :---------:  | :-------------------------------------: | :----------------------------------:|
| 1S | 2 | 2 |
| 2S | 2 | 8 |
| 2P | 6 | 8 |
| 3S | 2 | 18 |
| 3P | 6 | 18 |
| 3D | 10 | 18 |
| 4S | 2 | 32 |
| 4P | 6 | 32 |
| 4D | 10 | 32 |
| 4F | 14 | 32 |
| 5S | 2 | 50 |
| 5P | 6 | 50 |
| 5D | 10 | 50 |
| 5F | 14 | 50 |
| 5G | 18 | 50 |


Electrons generally fill the shells described above by what is called the [Aufbau principle](https://en.wikipedia.org/wiki/Aufbau_principle), in which the lower energy states will be occupied first. To find the order states will fill, first group levels by the sum of the sub-shell number $n$ with $l$. For instance; 3D, 4P, and 5S make a group as they all have $n+l = 5$. The lower $n+l$ states will be occupied first, and within these groups the lower sub-shells (n) will be occupied first. The order in which states fill is therefore 1S, 2S, 2P, 3S, 3P, 4S, 3D, 4P, 5S, 4D, 5P, 6S, and so on. To write the electron configuration of an atom we write out these sub-shells with a superscript to indicate the number of electrons occupying that sub-shell. For example, Mercury (Hg, atomic number 80) could have an electron configuration of $1s^22s^22p^63s^23p^64s^23d^{10}4p^65s^24d^{10}5p^66s^24f^{14}5d^{10}$. Often the full configuration is not written out, but an abbreviated form such as $[Xe]6s^24f^{14}5d^{10}$ or even just $6s^24f^{14}5d^{10}$ will be used. Further abbreviations include only writing the sub-shells which are not full.

# Spectroscopic Notation

We may write the state resulting from a given electron configuration in terms of the total intrinsic spin angular momentum s, the total orbital angular momentum *l*, and the total angular momentum *J*. We do this using spectroscopic notation which is written as $^{(2s+1)}L_J$, where $L$ is to be replaced with S, P, D, F, G according to the states total orbital angular momentum.

# Cursed Coupling Schemes

Reference "Bracket States in Yb'' by Wesley Campbell for a better discussion, but I will write a synopsis below as a summary and review for myself. When there are angular momentum contributions from multiple electron shells we must add the intrinsic spin angular momentum and orbital angular momentum of both shells. Therefore in considering LS coupling with two electron shells having angular momenta, $J=L+S$, $L=l_c+l_o$, and $S=s_c+s_o$ (where $c$ and $o$ stands for core shell and outer shell contributions, respectively). It is in these more complicated instances of addition of angular momenta that we often consider alternate coupling schemes, such as $J_1K$, $LK$, and $JJ$.

$J_1K$ couples $J_1=l_c+s_c$, $K=J_1+l_o$, and $J=K+s_o$. The $J_1K$ term symbol is written $^{2s_o+1}[K]_J$. 

The $LK$ coupling scheme couples $L=l_c+l_o$, $K=L+s_c$, and $J=L+K$. The $LK$ term symbol is written $L^{2s_o+1}[K]_J$. 

Finally $JJ$ couples $J_c=s_c+l_c$, $J_o=s_o+l_o$, and $J = J_c+J_o$. The $JJ$ term symbol is written $(J_1,J_2)_J$.

# Examples Reading Electron Configuration and Spectroscopic Notation

The below configurations can be found on the [NIST Atomic Spectra Database](https://physics.nist.gov/PhysRefData/ASD/levels_form.html) [Levels Data for Yb II](https://physics.nist.gov/cgi-bin/ASD/energy1.pl?de=0&spectrum=Yb+II&submit=Retrieve+Data&units=0&format=0&output=0&page_size=15&multiplet_ordered=0&conf_out=on&term_out=on&level_out=on&unc_out=1&j_out=on&lande_out=on&perc_out=on&biblio=on&temp=) (II for the second spectra of Yb, i.e. the spectra for singly ionized Yb). 

## Ground State
Let us begin with $4f^146s$ (sub-shells of lower energy not written are assumed to be filled). We see that in ionizing Yb has removed an electron from the $6s^2$ sub-shell, so now there is only a $6s$. With it being only one electron we know the intrinsic spin is 1/2, and the orbital angular momentum associated with the s sub-shell is 0, so by addition of angular momenta $J = L+S = 0 + 1/2 = 1/2$, and so our term symbol for this configuration's state is $^2S_{1/2}$.

## Excited State
For another example let us take the electron configuration $4f^{13}(^2F^o)6s^2$ of Yb$^+$. We know the $4f$ sub-shell holds up to 14 electrons, but here there are only 13. The f sub-shell here is missing an electron and thus forms our core with $s_c = 1/2$ for the one missing electron and $l_c=3$. The $6s^2$ does not contribute as the sub-shell is full. Therefore $J=s_c+l_c=7/2$ or $5/2$, and we may specify which state by writing either $^2F_{7/2}$ or $^2F_{5/2}$.

## Bracket ($J_1K$) State
Now let us take the configuration $4f^{13}(^2F^o_{7/2})5d6s(^3D)$ from Yb$^+$. We see the f sub-shell core is missing an electron such that in the $J_1K$ coupling scheme $s_c=1/2$, $l_c=3$, and $J_c=s_c+l_c= 7/2$ or $5/2$. The term in parenthesis immediately following the f sub-shell configuration $(^2F^o_{7/2})$ indicates the state has $J_c=7/2$. Now the outer shell consists of an electron in $6s$ and an electron in $5d$, such that $s_o=1/2+1/2= 0,1$. Likewise, we see that the $6s$ and $5d$ sub-shells contribute orbital angular momenta such that $l_o=0+2=2$. The term symbol immediately following $(^3D)$ tells us we are considering the state in which $3=2s_o+1$ such that $s_o=1$ and $l_o=2$. Using the $J_1K$ coupling scheme we find $K = J_c+l_o = 7/2+2 = 11/2,9/2,7/2,5/2,3/2$. Now the value of $K$ in a state will determine the possible values of $J$. For example, of the possible states with this configuration let us choose the one in which $K=3/2$. Then $J=K+s_o=3/2+1= 5/2,3/2,1/2$, and we may write these $^{2s_o+1}[K]_J$ term symbols as $^3[3/2]_{5/2}$, $^3[3/2]_{3/2}$, or $^3[3/2]_{1/2}$ depending on the total angular momentum $J$.