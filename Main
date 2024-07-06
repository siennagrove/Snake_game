import pygame
import random
p = pygame
p.init()

#screen setup 
width = 400
height = 300
block = 15
dis = p.display.set_mode((width, height))
p.display.set_caption('Snake game')

#colours
white = (255, 255, 255)
blue = (0, 0, 255)
black=(0,0,0)

#fonts
score_font = p.font.SysFont("menlo", 12)
gameover_font= p.font.SysFont("menlo",30)

#draws snake
def snake(block, snake_list):
    for x in snake_list:
        pygame.draw.rect(dis, blue, [x[0], x[1], block, block])

#text functions 
def score(score):
    value = score_font.render("Score: " + str(score),False, blue)
    dis.blit(value, [0, 0])

def end_game_message(you_lose, score, color):
    dis.fill(black)
    mesg1 = gameover_font.render(you_lose, True, color)
    mesg1_rect = mesg1.get_rect(center=(width / 2, height / 2 - 20))
    dis.blit(mesg1, mesg1_rect)
    mesg2 = gameover_font.render(score, True, color)
    mesg2_rect = mesg2.get_rect(center=(width / 2, height / 2 + 20))
    dis.blit(mesg2, mesg2_rect)

#main game function 
def gameLoop():
    game_over = False

    #starting snake in middle of the screen
    snake_x = (width // 2 // block)* block
    snake_y = (height // 2 // block) * block

    #snake updating position 
    snake_x_change = 0
    snake_y_change = 0
    
    #snake array setup to update size
    snake_list=[]
    snake_length= 1

    #food positioning
    food_x= round(random.randint(block*2, width-block)/block)*block
    food_y= round(random.randint(block*2, height-block)/block)*block

    while not game_over:
        #background colour
        dis.fill(white)

        #draw food
        p.draw.rect(dis, black, (food_x, food_y, block, block))

        #draw snake
        p.draw.rect(dis, blue, (snake_x, snake_y, block, block))
        snake(block, snake_list)

        for event in p.event.get():
            if event.type == p.QUIT:
                game_over = True 
            
            #updating snake position by key
            if event.type == p.KEYDOWN:
                #Left
                if event.key == p.K_LEFT:
                    snake_x_change = -block
                    snake_y_change = 0
                #Right
                elif event.key == p.K_RIGHT:
                    snake_x_change = block
                    snake_y_change = 0
                #Down
                elif event.key == p.K_DOWN:
                    snake_y_change = block
                    snake_x_change = 0
                #Up
                elif event.key == p.K_UP:
                    snake_y_change = -block
                    snake_x_change = 0

        snake_x+= snake_x_change
        snake_y += snake_y_change

        #snake head list with x and y of snake
        snake_head = []
        snake_head.append(snake_x)
        snake_head.append(snake_y)

        #snake head list added to snake list 
        snake_list.append(snake_head)

        #ensures the snake length is not greated than the snake list size
        if len(snake_list) > snake_length:
            del snake_list[0]
        
        #checks for self collision
        for segment in snake_list[:-1]:
            if segment == snake_head: 
                game_over = True

        #snake out of boundries 
        if snake_x >= width or snake_x < 0 or snake_y >= height or snake_y < 0:
            game_over = True

        

        #snake eating food
        if snake_x == food_x and snake_y == food_y:
             #new food
             food_x= round(random.randint(block*2,width-block*2)/block)*block
             food_y= round(random.randint(block*2,height-block*2)/block)*block
             #increased length
             snake_length +=1 
        #update score
        score(snake_length-1)
        p.display.update()
        p.time.delay(100)
   
    #if game over dislay message and quit 
    end_game_message("You lose!", "Final Score = " + str(snake_length-1), blue)
    p.display.update()
    p.time.delay(2000) 
    p.quit()
    quit()

gameLoop()

