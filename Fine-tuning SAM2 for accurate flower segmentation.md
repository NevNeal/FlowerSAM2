
- paper idea: [[Where are all the iNaturalists?]]

# To-Do:
- [ ] There are 417 angiosperm families in iNaturalist's taxonomy, but close to 500 flowering families recognized by the APG3, need to generate a list of the discrepencies
	- [ ] come up with an explanation for why this is??
	- [ ] look for papers that cover the odd nature of iNaturalist's internal taxonomy in botanical species
- [ ] generate figures:
	- [ ] Worst performing flowers (percentage of the 20 images where Lang-SAM2 finds no flowers)
		- This works because we do in fact have flower annotations on inaturalist, and those end up being some of the oldest observations on the platform
	- [ ] image size vs. the worst performing families
	- [ ] general distribution of families with less than 20 observations
- [ ] find out what Lang-SAM2 can do
	- [ ] can i get counts of segmentations and how?
		- [ ] in the highest counted families, would be really good to compare the number of visible flowers vs. how Lang-SAM2 did


text_prompt = "flower"

input_base = "/content/drive/MyDrive/research_grade_flower_images_2015_2024"

overlay_out = "/content/drive/MyDrive/research_grade_flower_overlays"

mask_out = "/content/drive/MyDrive/research_grade_flower_masks"

csv_path = "/content/drive/MyDrive/research_grade_flower_overlays/mask_summary.csv"

What kind of flowers does SAM2 have trouble with?
- Which families does it perform the worst on?
	- If there's an annotation with no segmentations, that's a point against it
Is there better representation across different families?
What are the best conditions for segmentations?

This describes all of the plant species, and how many genera are in each family (2016): https://www.biotaxa.org/Phytotaxa/article/download/phytotaxa.261.3.1/20598/0

- probably need to get all this data from gbif's currated list of research-grade inat data (this also has a cool citation)

I need:
- 10 random flower images from:
	- 20 random genera (this will only begin to eclipse the largest families):
	- if a genera has less than 20 observations with flowers, just skip it.
		- from 500 families

# Dataset descriptions:
20_obs_images_per_family_with_flowers_2015_2024.csv
- 20 random research-grade observations from 2015 to 2024 sampled from each iNaturalist-defined angiosperm family (417 families with taxa ID: 47125)
- sometimes there aren't that many research-grade observations for a family, in that case there are as many observations collected as possible from that family
- it should be noted that some of these observation ids can't be found on gbif because they're not licensed for reuse!
- Sometimes there are multiple images per observation
	- IFF there is only 1 image, and it comes back 


# 9/18/25
- Update: I'm just going to grab observation IDs from 20 flower-having observations per family. That should only be 10000

For reference:
# ID for flowering plants: 47125
# Search for Annotations

`&term_id=` - the annotation group

- **1**=Life Stage, **9**=Sex, **12**=Flowers and Fruits, **36**=Leaves, **17**=Alive or Dead, **22**=Evidence of Presence, **33** Established (pilot test in Reptiles/Amphibians only)

`&term_value_id=` - the value within the group

- **Life Stage:** **2**=Adult, **3**=Teneral, **4**=Pupa, **5**=Nymph, **6**=Larva, **7**=Egg, **8**=Juvenile, **16**=Subimago
- **Sex:** **10**=Female, **11**=Male, **20** Cannot Be Determined
- **Flowers and Fruits:** **13**=Flowers, **14**=Fruits or Seeds, **15**=Flower Buds, **21**=No Flowers or Fruits
- **Leaves:** **37**=Breaking Leaf Buds, **38**=Green Leaves, **39**=Colored Leaves, **40**=No Live Leaves
- **Alive or Dead:** **18**=Alive, **19**=Dead, **20**=Cannot Be Determined
- **Evidence of Presence:** **23**=Feather, **24**=Organism, **25**=Scat, **26**=Track, **27**=Bone, **28**=Molt, **29**=Gall, **30**=Egg, **31**= Hair, **32**=Leafmine, **35**=Construction
- **Established:** **34**=Not Established