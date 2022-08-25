"""
CFG Python project - Recipe book
"""

#First of all, it is necessary to import all the libraries
import requests 
import random


#The web_search is a function to make a request to the Edamam API with a personal id and key
def web_search(ingredient, meal_type,health):
    app_id=''
    key=''
    url = 'https://api.edamam.com/search?q={}&beta=true&app_id={}&app_key={}&mealType={}&health={}'.format(ingredient, app_id, key, meal_type,health)
    result=requests.get(url) 
    final_search=result.json() 
    return final_search['hits']

# The get_recipe function returns all recipes based on different user's choices
def get_recipe():
    n_ingredients = int(input('How many ingredients do you want to use? '))
    
    meal_preference = input('Do you have a preferred meal? Type y or n: ')
    if meal_preference == 'y':
        meal_type = input('Are you looking for breakfast, lunch or a dinner recipe? ')
    else:
        meal_type = random.choice(["breakfast", "lunch", "dinner"])
    
    health=random.choice(["dairy-free","gluten-free"])
    
    i = 1    
    ingredient_list = [] 
    while i <= n_ingredients:
        ingredient = input('Enter ingredient n.' + str(i) + ' : ')
        ingredient_list.append(ingredient)
        i += 1
    
    results = web_search(ingredient,meal_type,health)
    all_recipes=[] #creation of an empty list to order the recipes per calories
    for i in results:
        recipe = i['recipe']
        all_recipes.append(recipe['label'])
        all_recipes.append(int(recipe['calories']))
        all_recipes.append(recipe['url']) 
        all_recipes.append(meal_type)
    N = 4
    subList = [all_recipes[n:n+N] for n in range(0, len(all_recipes), N)]       
    ordered_list = sorted(subList, key=lambda x: x[1], reverse=False)
    
    #saving the recipe with the lowest amount of calories into a txt file
    with open('recipe_book.txt','a') as text_file:
        for element in ordered_list[0]:
            recipe_book= str(element) + '\n' 
            text_file.write(recipe_book)
        for ingredient in recipe['ingredientLines']:
            recipe_book2 = ingredient  + '\n'
            text_file.write(recipe_book2)
            
    print('The list of recipes ranked by calories is the following:')
    for element in ordered_list:
        for sub_element in element:
            print(sub_element) 
            
     
get_recipe()

