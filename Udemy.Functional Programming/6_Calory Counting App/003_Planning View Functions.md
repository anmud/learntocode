# Planning View Functions

What `view functions` do we need to transform our `data model` into `html` and `css`? 

1. At a minimum we'll need the main `view function`, that will be responsible for returning everything we see in our `calorie app`. 

![view-function](../view-function.png)

2. Next we;ll have the `formView` function that will either show the `add meal button` or the `form`. 

![button-function](../button-function.png)
![form-function](../form-function.png)

3. Within the `formView` area we'll create a function that will create the `label` and `input field` combination, we'll call this function `fieldSet`. 

![field-set-function](../field-set-function.png)

4. Next we'll create a fucntion to generate the `form buttons`, which we'll call `buttonSet`. 

![button-set-function](../button-set-function.png)

5. For the `table section` we'll need the following: 

- a `tableView function` 

![table-view-function](../table-view-function.png)

- a `tableHeader constant` for the header area

![table-header-constant](../table-header-constant.png)

- a `mealsBody function` for the following area: 

![meals-body-function](../meals-body-function.png)

- a `mealRow function` for the rows: 

![meal-row-function](../meal-row-function.png)

- a `cell` function for each individual cell: 

![cell-calorie-function](../cell-calorie-function.png)

- a `totlaRow function` 

![total-calorie-row-function](../total-calorie-row-function.png)


