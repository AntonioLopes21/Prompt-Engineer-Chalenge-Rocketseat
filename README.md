# Prompt-Engineer-Chalenge-Rocketseat
https://docs-rocketseat.notion.site/Desafio-Prompt-Engineering-195395da5770805dbd67e3bd6f2d3fcc

#Desafios propostos
![image](https://github.com/user-attachments/assets/e7589780-90f3-460d-afff-d3bf7001b20d)

Desafio 1 - ChatGPT
![image](https://github.com/user-attachments/assets/5108a3c0-219f-455d-9479-6ac0db6df17b)
![image](https://github.com/user-attachments/assets/b80826bc-3b18-4361-a75b-01996d4ad585)
![image](https://github.com/user-attachments/assets/477aca65-942b-4493-af2e-3139d3fba82e)

Desafio 2 - Deepseek
![image](https://github.com/user-attachments/assets/58c8cd18-c7f3-4928-8cf4-eaed8c6f9f18)

Desafio 3 - ChatGPT
![image](https://github.com/user-attachments/assets/064d3e68-abcc-4f74-a45e-834646529e1a)
![image](https://github.com/user-attachments/assets/fdd4b3ac-453a-4e15-b691-3e2eabbaf3c3)
![image](https://github.com/user-attachments/assets/055cc88f-41fc-49bb-afdb-caadcadb3a0c)

Desafio 4 - Deepseek
![image](https://github.com/user-attachments/assets/bf14ba9c-bdbf-4ffe-9531-294b81bc87b1)

```
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field, validator
from datetime import date, datetime
from uuid import uuid4
from typing import Optional

app = FastAPI()

class Item(BaseModel):
    nome: str = Field(..., max_length=25)
    valor: float
    data: date
    
    @validator('data')
    def data_nao_pode_ser_futura(cls, v):
        if v > date.today():
            raise ValueError('A data não pode ser superior à data atual')
        return v

class ItemResponse(Item):
    uuid: str

@app.post("/items/", response_model=ItemResponse)
async def process_item(item: Item):
    """
    Processa um item, validando os dados e adicionando um UUID único.
    
    - **nome**: string com até 25 caracteres
    - **valor**: número float
    - **data**: data que não pode ser no futuro
    """
    # Gera um UUID único
    item_dict = item.dict()
    item_dict['uuid'] = str(uuid4())
    
    return item_dict
```
# Para testar localmente
```
if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)

```
![image](https://github.com/user-attachments/assets/43a1d703-d3f6-4b60-8c32-31a8fa872d51)
![image](https://github.com/user-attachments/assets/c5fea87e-8520-4d02-aa0b-95b023206edc)
