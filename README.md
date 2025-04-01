Вот код:

def read_recipe(file_name):
    cook_book = {}
    
    try:
        f = open(file_name, 'r', encoding='utf-8')
        lines = f.readlines()
        
        i = 0
        while i < len(lines):
            dish_name = lines[i].strip() 
            i += 1
            
            
            try:
                ingredients_count = int(lines[i].strip()) 
            except ValueError:
                print(f"Ошибка: ожидалось число в строке с количеством ингредиентов для '{dish_name}'")
                break
            i += 1
            
            ingredients = []
            for j in range(ingredients_count):
                
                if i >= len(lines):
                    print(f"Ошибка: недостающие данные для ингредиентов блюда '{dish_name}'")
                    break
                ingredient_info = lines[i].strip().split(" | ")
                if len(ingredient_info) != 3:
                    print(f"Ошибка: неправильный формат строки ингредиента для блюда '{dish_name}' на строке {i+1}")
                    break
                
                ingredient = {
                    'ingredient_name': ingredient_info[0],
                    'quantity': int(ingredient_info[1]),
                    'measure': ingredient_info[2]
                }
                ingredients.append(ingredient)
                i += 1
            
            cook_book[dish_name] = ingredients
        f.close()
    
    except FileNotFoundError:
        print(f"Файл {file_name} не найден!")
        return {}
    
    return cook_book
