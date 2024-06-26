### Useful codes
`adult['Marital Status'].value_counts(normalize=True)`
`adult.dtypes`


Set value to categorical
`adult["Marital Status"] = adult['Marital Status'].astype("category")`

Create categorical series
```
my_data = ["A", "A", "C", "B", "C", "D"]
my_series1 = pd.Series(my_data, dtype="Category")
my_series2 = pd.Categorical(my_data, categories=["C", "B", "A"], ordered=True)

# Categorical values saves more memory
```

Specifying `dtypes` when reading data
```
# create a dictionary
adult_dtypes = {"Marital Status": "category"}

# set dtype parameter
adult = pd.read_csv("data/adult.csv", dtype=adult_dtypes)

# check the dtype
adult["Marital Status"].dtypes
```

The basics of `.groupby()`: splitting data
```
adult = pd.read_csv("data/adult.csv)
adult1 = adult[adult["Above/Below 50k] == " <=50k"]
adult2 = adult[adult["Above/Below 50k] == " >50k"]

# is replaced by
groupby_object = adult.groupby(by=["Above/Below 50k"])

# apply functions
groupby_object.mean()

# one liner
adult.groupby(by=["Above/Below 50k"]).mean()



# specifying columns
# option 1: only runs .sum() on two columns (PREFERRED WAY)
adult.groupby(by=["Above/Below 50k"])['Age', 'Education Num'].sum()

# option 2: runs .sum() on all numeric columns and then subsets
adult.groupby(by=["Above/Below 50k"]).sum()[['Age', 'Education Num']]
```

Grouping with multiple columns
```
adult.groupby(by=["Above/Below 50k", "Marital Status"]).size()
```

`.cat` accessor object
`Series.cat.method_name`

Common parameters
	`new_categories`: a list of categories
	`inplace`: Boolean - whether or not the update should overwrite the Series
	`ordered`: Boolean - whether or not the categorical is treated as an ordered categorical

Setting series categories
- Can be used to set the order of categories
- All values not specified in this method are dropped
```
dogs["coat"] = dogs["coat"].cat.set_categories(
	new_categories=["short", "medium", "long"]
)

# setting order
dogs["coat"] = dogs["coat"].cat.set_categories(
	new_categories=["short", "medium", "long"],
	ordered=True
)
```

Adding categories
- Does not change the value of any data in the DataFrame
- Categories not listed in this method are left alone
```
dogs["likes_people"] = dogs["likes_people"].astype("category")
dogs["likes_people"] = dogs["likes_people"].cat.add_categories(
	new_categories=["did not check", "could not tell"]
)
```

Removing categories
- Values matching categories listed are set to `NaN`
```
dogs["coat"] = dogs["coat"].astype("category")
dogs["coat"] = dogs["coat"].cat.remove_categories(
	removals=["wirehaired"]
)
```

Renaming categories
```
# method
Series.cat.rename_categories(new_categories=dict)

# make a dictionary
my_changes = {"Unknown Mix": "Unknown"}

# rename category
dogs["breed"] = dogs["breed"].cat.rename_categories(my_changes)
```

Renaming categories with a function
```
dogs["sex"] = dogs["sex"].cat.rename_categories(lambda C: c.title())
```

Common replacement issues
- Must use new category names
- Cannot collapse two categories into one

Collapsing categories setup
```
dogs["color"] = dogs["color"].astype("category")

# create dictionary and use .replace
update_colors = {
	"black and brown": "black",
	"black and tan": "black",
	"balck and white": "black"
}

dogs["main_color"] = dogs["color"].cat.raplace(update_colors)

# convert back to categorical
dogs["main_color"] = dogs["main_color"].astype("category") 
```

Reordering example
```
dogs["coat"] = dogs["coat"].cat.reorder_categories(
	new_categories=["short", "medium", "wirehaired", "long"],
	ordered=True
)

# using `inplace`
dogs["coat"].cat.reorder_categories(
	new_categories=["short", "medium", "wirehaired", "long"],
	ordered=True,
	inplace=True
)
```


### Cleaning and accessing data
Identify issues, use either:
- `Series.cat.categories`
- `Series.values_counts()`

Fixing issues: 
```
# whitespaces
# removing whitespaces: `.strip()`
dogs["get_along_cats"] = dogs["get_along_cats"].str.strip()

# capitalization
# using `.title()`, `.upper()`, `.lower()`
dogs["get_along_cats"] = dogs["get_along_cats"].str.title()

# mispelled words
# fixing type with `.replace()`
replace_map = {"Noo": "No"}
dogs["get_along_cats"].replace(replace_map, inplace=True)
```

### Using `str` accessor object
Searching for a string
`dogs["breed"].str.contains("Sheperd", regex=False)`

Access Series values based on category
`dogs.loc[dogs["get_along_cats"] == "Yes", "size"]`

Series value counts
`dogs.loc[dogs["get_along_cats"] == "Yes", "size"].value_counts(sort=False)`

### Categorical plots using Seaborn
Categorical Plots
```
import seaborn as sns
import matplotlib.pyplot as plt

sns.catplot(...)
plt.show()
```

The catplot parameters
- `x, y`: name of variable in data
- `data`: a DataFrame
- `kind`: type of plot to create - one of: `"strip"`, `"swarm"`, `"box"`, `"violin"`, `"boxen"`, `"point"`, `"bar"`, or `"count"`

Example
```
sns.catplot(
    x="Traveler type",
    y="Helpful votes",
    data=reviews,
    kind="box"
)
```

```
# setting font size and plot background
sns.set(font_scale=1.4)
sns.set_style("whitegrid"),
```

Traditional bar chart
```
reviews["Traveler type"].value_counts().plot.bar()
```

Hue parameter
- `hue`:
	- name of a variable in `data`
	- used to split the data by a second category
	- also used to color the graphic
```
sns.set(font_scale=1.2)
sns.set_style("darkgrid")
sns.catplot(x="Traveler type", y="Score", data=reviews, kind="bar", hue="Tennis court")
```

New parameter for point plot
`dodge`: Boolean - to not overlap visual
`join`: Boolean - to not connect the lines


### Additional `catplot()` options
Using the `catplot() facetgrid`
```
sns.catplot(
	x="Traveler type", 
	kind="count", 
	col="User continent",
	col_wrap=3,
	palette=sns.color_palette("Set1"),
	data=reviews
)
```

Updating plots
- Setup: save your graphic as an object: `ax`
- Plot title: `ax.fig.suptitle("My title")`
- Axis labels: `ax.set_axis_labels("x-axis-label", "y-axis-label")`
- Title height: `plt.subplots_adjust(top=0.9)`


### Label encoding
Creating codes
`used_cards["manufacturer_name"] = used_cars["manufacturer_name"].astype("category")`

Use `.cat.codes`

#### Creating a code book
```
codes = used_cars["manufacturer_name"].cat.codes
categories = used_cars["manufacturer_name"]

name_map = dict(zip(codes, categories))


# creating codes
used_cars["manufacturer_code"] = used_cars["manufacturer_name"].cat.codes

# reverting to previous values
used_cars["manufacturer_code"].map(name_map)
```

Boolean coding
```
used_cars["body_type"].str.contains("van", regex=False)

# create a boolean coding
used_cars["van_code"] = np.where(
	used_cars["body_type"].str.contains("van", regex=False), 1, 0
)
```


### One-hot encoding with pandas
`pd.get_dummies`
- `data`: a `pandas` DataFrame
- `columns`: a list-like object of column names
- `prefix`: a string to add to the beginning of each category

Example
```
used_cars_onehot = pd.get_dummies(used_cars[["odometer_value", "color"]])

# specifying columns to use
used_cars_onehot = pd.get_dummies(used_cars, columns=["color"], prefix="")
```