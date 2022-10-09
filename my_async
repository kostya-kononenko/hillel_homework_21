import asyncio
import aiohttp
import time


async def api_task(url, session):
    response = await session.request(method='GET', url=url)
    return await response.json()


async def currency_api(url, session):
    result = await api_task(url, session)
    return float(result['eur']['uah'])


async def economia_awesome(url, session):
    result = await api_task(url, session)
    return float(result['EURUAH']['ask'])


async def exchangerate(url, session):
    result = await api_task(url, session)
    return float(result['rates']['UAH'])


async def main():
    async with aiohttp.ClientSession() as session:
        results = await asyncio.gather(*[
            currency_api("https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/eur.json", session),
            economia_awesome("https://economia.awesomeapi.com.br/json/last/EUR-UAH", session),
            exchangerate("https://api.exchangerate.host/latest", session),
        ])
        return round(sum(results)/len(results), 7)

start = time.time()
print(f"Average UAH to EUR exchange rate today {asyncio.run(main())}")
print(f"program took {time.time() - start} to finish")