# Defined functions

---
    def csv_path(file_csv):
        file = []
        with open(os.path.join(__location__, f'{file_csv}.csv')) as f:
            rows = csv.DictReader(f)
            for i in rows:
                file.append(dict(i))
        return file

    def insert_row(self, dict):
            '''
            This method inserts a dictionary, dict, into a Table object, effectively adding a row to the Table.
            '''
            self.table.append(dict)

    def update_row(self, primary_attribute, primary_attribute_value,
                   update_attribute, update_value):
        '''
        This method updates the current value of update_attribute to update_value
        For example, my_table.update_row('Film', 'A Serious Man', 'Year', '2022') will change the 'Year' attribute for the 'Film'
        'A Serious Man' from 2009 to 2022
        '''
        for i in self.table:
            if i[primary_attribute] == primary_attribute_value:
                i[update_attribute] = update_value
---
# Find the average value of ‘Worldwide Gross’ for ‘Comedy’ movies
    only_comedy = movies.filter(lambda x: x["Genre"] == "Comedy")
    world_gross = only_comedy.aggregate(lambda x: sum(x) / len(x),
                                        "Worldwide Gross")
---
# Find the minimum ‘Audience score %’ for ‘Drama’ movies
    only_drama = movies.filter(lambda x: x["Genre"] == "Drama")
    score = only_drama.aggregate(lambda x: min(x), "Audience score %")
---
# Insert the following movie
    dict = {}
    dict['Film'] = 'The Shape of Water'
    dict['Genre'] = 'Fantasy'
    dict['Lead Studio'] = 'Fox'
    dict['Audience score %'] = '72'
    dict['Profitability'] = '9.765'
    dict['Rotten Tomatoes %'] = '92'
    dict['Worldwide Gross'] = '195.3'
    dict['Year'] = '2017'
    movies.insert_row(dict)
---
# Update the  'Year' for the  'Film' :  'A Serious Man' to '2022'
    movies.update_row('Film', 'A Serious Man', 'Year', '2022')
