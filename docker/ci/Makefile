 CONTAINER := python_task1
 
build:
	@docker-compose up -d
 
composer:
	@docker exec -i $(CONTAINER) composer install
 
test:
	@docker exec -i $(CONTAINER) /tests test.py
	@make -s down
 
down:
	@docker-compose down --volumes
	@make -s clean
 
clean:
	@docker system prune --volumes --force
