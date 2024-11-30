# Guía stats in-game

## Introducción
A partir de ahora, se podrán aplicar efectos, atributos y modificadores al combate según los puntos de las stats.

¿Cómo se aplican los efectos?
- Los efectos de pociones y cambios de atributos (más vida, velocidad, etc), se aplican al conectarte o cambiarte de personaje, por ahora no hay un comando que refresque estos efectos hasta que no esté bien testado el sistema

¿Cómo funciona el escalado de los efectos?
- Simple, usando el valor de la configuración `effects-stat-power`, por ejemplo, con el valor en 1, si tenemos configurado que agilidad nos da el efecto de velocidad, y tenemos un personaje con 15 en agilidad, recibiremos el efecto de velocidad potenciado a 15. Es lo recomendado, pero se puede modificar 

¿Cómo se puede probar esto sin reiniciar todo el rato y hacer la configuración inicial?

**Es muy importante probar bien antes de quitar la lista y ponerlo para todos los jugadores**
- Para poder hacer pruebas y no afectar a los usuarios normales, se usan dos cosas:
   - Lista de filtrado: Si añadimos players, solo se le aplicarán los efectos a esos jugadores
   - El comando `rpkcharactersreloadconfig` nos permite recargar esta configuración sin necesidad de reiniciar el servidor

## Configuración
El fichero con las configuraciones está en -> `plugins\rpk-characters-bukkit\config.yml`

Estando en el fichero, buscaremos la sección de `stats` que tendrá el siguiente formato:
```
stats:
  players: # Whitelist para aplicar los efectos, si no tiene nombres, se aplicaran a todos los jugadores
    - FrostFire
    - Jesus
    - Antoñito
  effects-stat-power: 1 # Escalado para los efectos de pociones y atributos, recomendado en 1 = 1 * level atributo
  effects:  # Listado de los efectos y atributos que se aplican y para que atributo
    Inteligencia: velocidad # Se debe colocar en formato NombreStat : NombreDelEfecto
    Fuerza: velocidad_ataque
  combat-stat-power: 1 # Escalado para los efectos de combate custom, ahora mismo no hace nada, pero puede que se use a futuro
  combat: # Listado de los efectos custom de combate
    Destreza: critico  # Se debe colocar en formato NombreStat : NombreDelEfecto
```




# Modificadores

## Efectos de Pociones

| **Nombre**|**Nombre Config**|**Descripción**|**Tipo**|
|-------------------------|------------------------|--------------------------------------------------|-------------------------------|
| SPEED                  | velocidad             | Aumenta la velocidad de movimiento                | PotionEffectType.SPEED        |
| SLOWNESS               | lentitud              | Reduce la velocidad de movimiento                 | PotionEffectType.SLOW         |
| HASTE                  | prisa                 | Aumenta la velocidad de minería                   | PotionEffectType.FAST_DIGGING |
| MINING_FATIGUE         | fatiga                | Reduce la velocidad de minería                    | PotionEffectType.SLOW_DIGGING |
| STRENGTH               | fuerza                | Aumenta el daño cuerpo a cuerpo                   | PotionEffectType.INCREASE_DAMAGE |
| INSTANT_HEALTH         | curacion              | Restaura salud al instante                        | PotionEffectType.HEAL         |
| INSTANT_DAMAGE         | daño_instantaneo      | Inflige daño al instante                          | PotionEffectType.HARM         |
| JUMP                   | salto                 | Incrementa la altura de los saltos                | PotionEffectType.JUMP         |
| NAUSEA                 | nausea                | Desorienta visualmente                            | PotionEffectType.CONFUSION    |
| REGENERATION           | regeneracion          | Restaura salud con el tiempo                      | PotionEffectType.REGENERATION |
| RESISTANCE             | resistencia           | Reduce el daño recibido                           | PotionEffectType.DAMAGE_RESISTANCE |
| FIRE_RESISTANCE        | resistencia_fuego     | Inmunidad al daño por fuego                       | PotionEffectType.FIRE_RESISTANCE |
| WATER_BREATHING        | respiracion           | Permite respirar bajo el agua                     | PotionEffectType.WATER_BREATHING |
| INVISIBILITY           | invisibilidad         | Vuelve al jugador invisible                       | PotionEffectType.INVISIBILITY |
| BLINDNESS              | ceguera               | Reduce la visión del jugador                      | PotionEffectType.BLINDNESS    |
| NIGHT_VISION           | vision_nocturna       | Permite ver en la oscuridad                       | PotionEffectType.NIGHT_VISION |
| HUNGER                 | hambre                | Aumenta el consumo de alimentos                   | PotionEffectType.HUNGER       |
| WEAKNESS               | debilidad             | Reduce el daño cuerpo a cuerpo                    | PotionEffectType.WEAKNESS     |
| POISON                 | veneno                | Inflige daño con el tiempo                        | PotionEffectType.POISON       |
| WITHER                 | wither                | Inflige daño con el tiempo y ennegrece la vista   | PotionEffectType.WITHER       |
| HEALTH_BOOST           | vida_extra            | Incrementa la salud máxima                        | PotionEffectType.HEALTH_BOOST |
| ABSORPTION             | absorcion             | Añade corazones temporales                        | PotionEffectType.ABSORPTION   |
| SATURATION             | saturacion            | Restaura la barra de hambre                       | PotionEffectType.SATURATION   |
| GLOWING                | brillo                | Hace al jugador visible                           | PotionEffectType.GLOWING      |
| LEVITATION             | levitacion            | Eleva al jugador                                  | PotionEffectType.LEVITATION   |
| LUCK                   | suerte                | Incrementa la probabilidad de encontrar objetos valiosos | PotionEffectType.LUCK |
| BAD_LUCK               | mala_suerte           | Reduce la probabilidad de encontrar objetos valiosos | PotionEffectType.UNLUCK |
| DOLPHINS_GRACE         | gracia_delfin         | Incrementa la velocidad de nado                   | PotionEffectType.DOLPHINS_GRACE |
| SLOW_FALLING           | caida_lenta           | Reduce la velocidad de caída                      | PotionEffectType.SLOW_FALLING |
| CONDUIT_POWER          | poder_conducto        | Mejora habilidades acuáticas                      | PotionEffectType.CONDUIT_POWER |
---
## Atributos
|**Nombre**|**Nombre Config**|**Descripción**|**Tipo**|
|------------------------|-----------------------|---------------------------------------------------|-------------------------------|
| DAMAGE                 | daño                  | Aumenta el daño base                              | Attribute.GENERIC_ATTACK_DAMAGE |
| KNOCKBACK_RESISTANCE   | resistencia_empuje    | Reduce el efecto de empuje                        | Attribute.GENERIC_KNOCKBACK_RESISTANCE |
| MOVEMENT_SPEED         | velocidad             | Aumenta la velocidad de movimiento                | Attribute.GENERIC_MOVEMENT_SPEED |
| HEALTH                 | vida                  | Incrementa la salud máxima                        | Attribute.GENERIC_MAX_HEALTH   |
| ATTACK_SPEED           | velocidad_ataque      | Incrementa la rapidez al atacar                   | Attribute.GENERIC_ATTACK_SPEED |
| ARMOR                  | armadura| Incrementa la protección contra daño              | Attribute.GENERIC_ARMOR        |
| ARMOR_TOUGHNESS        | resistencia_armadura  | Reduce el daño penetrante     | Attribute.GENERIC_ARMOR_TOUGHNESS
---
## Efectos de combate
| **Nombre**| **Nombre Config**| **Descripción**|
|-------------------------|------------------------|--------------------------------------------------|
| Critico del lolillo | critico | Aumenta el dañó en 175%                              

