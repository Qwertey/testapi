from typing import List
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    data: List[List[float]] = []
    ratio: int

@app.post("/pattern1/")
async def create_item(item: Item):
    data = item.data
    ratio = item.ratio
        # Your existing logic here
    
    if data[2][0] > data[2][1] > data[2][2] < data[2][3] < data[2][4] and data[2][3] < data[2][0]:#and df["Open"][i+2] < df["Close"][i+4]:
        #position
        position="long"
        #stop_loss
        st_price = min(data[1][:4])
        #Close price of taken trade
        close_price = data[2][4]
        #points of stop_loss
        points = close_price - st_price
        #target price
        target_price = close_price + (points*ratio)
        target_price = round(target_price,2)
        #Percentage change for st and close
        perc_change_st = -(((st_price - close_price) / close_price) * 100)
        
        return [position,st_price,close_price,target_price,perc_change_st]
        
    
    elif data[2][0] < data[2][1] < data[2][2] > data[2][3] > data[2][4] and data[2][3] > data[2][0]:# and df["Open"][i+2] > df["Close"][i+4] :
        #position
        position="short"
        #Stop_loss_price
        st_price = max(data[0][:4])
        #Close price of taken trade
        close_price = data[2][4]
        #points of stop_loss
        points = st_price - close_price
        #target price
        target_price = (close_price - (points*ratio))
        target_price = round(target_price,2)
        #Percentage change for st and close
        perc_change_st = (((st_price - close_price) / close_price) * 100)
        
        return [position,st_price,close_price,target_price,perc_change_st]
        
    else:
        return None
