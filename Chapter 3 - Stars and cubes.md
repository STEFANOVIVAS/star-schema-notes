# Chapter 3 - Stars and cubes

## Dimension Table Features

### Surrogate Keys and Natural Keys

- Surrogate keys are created especially for the data warehouse or data mart and have a unique value (Generally integers).
- The use of surrogate keys as unique identifiers allows the data warehouse to respond to changes in source data in whatever manner best fits analytic requirements.
- Natural keys are identifiers carried over from source systems and may have meaning to users of the data warehouse.
- When more than one system can be the source for a dimension, the natural key may be composed of the identifier from the source system and an additional identifier that indicates which source it came from (Ex.: mergers and acquisitions leading to different source systems).

### Rich Set of Dimensions
