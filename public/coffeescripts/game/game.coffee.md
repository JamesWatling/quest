# Development Game File

This file is where we use quest to create things to make sure that they are working.

<!-- -->

    canvas = document?.getElementById 'gameCanvas'
    context = canvas.getContext '2d'

    box =
      width: 10
      height: 10
      speed: 2
      color: '#b8703a'
      pos:
        x: canvas.width/2 - 5
        y: canvas.height/2 - 5
      vel:
        x: 0
        y: 0

    keys =
        38:  # up
          pressed: false
          press: -> box.vel.y += box.speed
          release: -> box.vel.y -= box.speed
        40: # down
          pressed: false
          press: -> box.vel.y -= box.speed
          release: -> box.vel.y += box.speed
        37: # left
          pressed: false
          press: -> box.vel.x += box.speed
          release: -> box.vel.x -= box.speed
        39: # right
          pressed: false
          press: -> box.vel.x -= box.speed
          release: -> box.vel.x += box.speed

    Q.events.register 'keydown', (e) ->
      code = e.which ? e.keyCode
      if keys[code]? and not keys[code]?.pressed
        keys[code].pressed = true
        keys[code].press()
    Q.events.register 'keyup', (e) ->
      code = e.which ? e.keyCode
      if keys[code]? and keys[code]?.pressed
        keys[code].pressed = false
        keys[code].release()

    do updateFrame = ->
      requestAnimationFrame updateFrame

      context.clearRect 0, 0, canvas.width, canvas.height

      box.pos.x -= box.vel.x
      box.pos.y -= box.vel.y

      context.fillStyle = box.color
      context.fillRect box.pos.x, box.pos.y, box.width, box.height