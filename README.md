# Project-One

import pymongo

# class MongoDB
class MongoDB:
    # constructor 
    def __init__(self, database, collection):
        self.client = pymongo.MongoClient()
        self.database = self.client[database]
        self.collection = self.database[collection]
        
    # create method
    def create(self, data):
        try:
            result = self.collection.insert_one(data)
            return True
        except:
            return False
    # read method  
    def read(self, query):
        try:
            cursor = self.collection.find(query)
            return cursor
        except Exception as e:
            return str(e)
    
    # update method  
    def update(self, query, data):
        try:
            result = self.collection.update_many(query, {'$set': data})
            return result.raw_result
        except Exception as e:
            return str(e)
      
    # delete method  
    def delete(self, query):
        try:
            result = self.collection.delete_many(query)
            return result.raw_result
        except Exception as e:
            return str(e)
