
  import discord
from discord.ext import commands
import requests

# Создание экземпляра бота
bot = commands.Bot(command_prefix='!')

# Функция для получения информации о рок-группе
def get_band_info(band_name):
    # Здесь вы можете использовать API, например, Last.fm или Wikipedia API
    # Для примера просто вернем фиксированные данные
    bands_data = {
        'Nirvana': {
            'description': 'Nirvana was an American rock band formed in Aberdeen, Washington, in 1987. They are credited with bringing grunge music to the mainstream.',
            'image_url': 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Nirvana_%28band%29.jpg/800px-Nirvana_%28band%29.jpg'
        },
        'Queen': {
            'description': 'Queen is a British rock band formed in London in 1970. The group is known for its eclectic style and theatrical performances.',
            'image_url': 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/Queen_%28band%29.jpg/800px-Queen_%28band%29.jpg'
        },
        # Добавьте больше групп по аналогии
    }
    
    return bands_data.get(band_name)

@bot.command()
async def band(ctx, *, band_name: str):
    band_info = get_band_info(band_name)
    
    if band_info:
        embed = discord.Embed(title=band_name, description=band_info['description'])
        embed.set_image(url=band_info['image_url'])
        await ctx.send(embed=embed)
    else:
        await ctx.send("Извините, информация о такой группе не найдена.")

# Запуск бота
bot.run('8042347481:AAHxK6JUrXu1xDxd4pxmMwt5O-qRlfnTqKA')
