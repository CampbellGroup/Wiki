Ultrahigh vacuum requires care during every step of the assembly process. 

# Designing for vacuum

## Best practices
- ALWAYS consult the vacuum-safe materials list given below.
	- If something isn't on the list, you can do an outgassing test in a test-chamber, or consult [LIGO](https://dcc.ligo.org/LIGO-E960050-v12/public) 
- Avoid blind tapped holes, as air can get trapped under a screw and cause a slow virtual leak. If you do have blind tapped holes, use a vented screw to allow the air to escape. 
- When machining or having parts machined, use the smoothest surface finish you can to minimize surface area. (There's a reason that stock vacuum parts are so shiny)
- When making a tight connection, like a screw in a thread, using dissimilar metals (like a gold-plated bolt in a stainless thread) can prevent sticking and seizing
- Avoid long runs of wire where possible, as they are susceptible to noise and can move during bakeout due to thermal expansion
## Vacuum-safe materials
### Whitelist
Here is a list of materials that work in vacuum. This is cobbled together from [wikipedia](https://en.wikipedia.org/wiki/Materials_for_use_in_vacuum#Review_of_materials_and_issues_to_consider), [LIGO](https://dcc.ligo.org/LIGO-E960050-v12/public), and our experiences as a lab. 
- Metals
	- Stainless steel
		- 304 is fine
		- 304L is the best in general
		- 316L is low-magnetic
	- Aluminium and aluminium alloys, as long as the alloys don't contain any zinc. Must not be anodized. During a hot bake thin parts can deform under load. 
		- 6061 (the most common alloy for machining) is fine. 
	- Copper
		- Oxygen-free copper should be used wherever possible, as it has much better outgassing properties. During a hot bake thin parts can deform under load.  
	- Gold
	- Platinum
	- Tungsten
	- Titanium
	- Molybdenum
	- Invar
	- Beryllium copper (common in electrical connectors)
	- Aluminum bronze
- Ceramics
	- Alumina - go for the high purity stuff
	- Macor
	- Steatite - I've used accu-glass' steatite beads for wire insulation and it seems to work
	- Glass
	- Sapphire
- Tin-silver solder (if you must)
- Plastics
	- PEEK (polyetheretherketone). As a rule, use PEEK where you can, and use Kapton where you can't
	- Kapton (polyimide film)
	- Maybe other polyimide plastics?
- Adhesives
	- Accu-glass' UHV epoxy (EPO-TEK 353ND)
### Blacklist
- Anything containing Zinc
	- 7xxx series aluminum
	- most brass
- Cadmium
- Most plastics, unless listed above
- Solder, unless listed above
- Grease
- Polishing and abrasive compounds
# Cleaning
When cleaning, start with lower vapor pressure solvents and work up to higher vapor pressure solvents. 
Here's the sequence, with 30 or so minutes of sonication in each step. 
1) dilute (~$1/10^{th}$ recommended on the box) alconox
2) deionized or distilled water
3) isopropanol
4) methanol
5) acetone
The process for cleaning with each of these solvents is the same and outlined below.
1) Fill a sonicator basin with tap water.
2) Place the parts in a beaker and fill it with the cleaning solution. 
	- Flammable solvents (such as methanol or acetone) should never be poured directly into the sonicator basin.
3) Cover the beaker with an aluminum foil lid (especially for more volatile solvents). Dent the lid down in the middle so evaporated gasses will condense and return to the beaker, and try not to let the aluminum foil get in the sonicator water.
4) Run the sonicator at a warm temperature (~40 degress Celcius) for 30 minutes. Higher frequencies are better for smaller parts.
5) Pour the used solution into a waste container specific to that solvent. 
6) Wrap the parts in UHV foil and let dry before moving to the next cleaning stage. 
	- Alternatively blow dry using dry nitrogen, or heat dry in a clean oven
# Assembly
Tightening bolts on a vacuum chamber:
1) Place a gasket on the knife edge of the flange.
2) We generally use silver bolts (purchased from Duniway). Loosely finger-tighten the bolts.
3) With the parts held loosely in place, tighten the bolts in a star pattern. Ideally each bolt should have about the same resistance and should be turned by about (~1/4 turn to ~1/8 turn) as you iterate through this star pattern multiple times until it is tight with even pressure along the gasket. Google "flange tightening pattern" if you cannot find below the match to your flange.

![[Pasted image 20240227153744.png]]
