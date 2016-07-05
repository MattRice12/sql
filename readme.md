SELECT SUM(salary) from family_members;
SELECT COUNT(*) FROM friends_of_pickles WHERE species = 'dog';
SELECT * FROM friends_of_pickles ORDER BY height_cm DESC LIMIT 1;
SELECT DISTINCT species FROM friends_of_pickles WHERE height_cm > 50;

SELECT MAX(height_cm), species FROM friends_of_pickles GROUP BY species;


##select family_member with the highest salary
  SELECT * FROM family_members WHERE salary = (SELECT MAX(salary) FROM family_members);

SELECT * FROM family_members WHERE favorite_book IS NOT NULL;

SELECT * FROM celebs_born WHERE birthdate > '1980-09-01';


##Can you use an inner join to pair each character name with the actor who plays them? Select the columns: character.name, character_actor.actor_name

  SELECT character.name, character_actor.actor_name FROM character
  INNER JOIN character_actor
  ON character.id = character_actor.character_id;


##Can you use two joins to pair each character name with the actor who plays them? Select the columns: character.name, actor.name
  SELECT character.name, actor.name
  FROM character
  INNER JOIN character_actor
  ON character.id = character_actor.character_id
  INNER JOIN actor
  ON character_actor.actor_id = actor.id;

##Can you use left joins to match character names with the actors that play them? Select the columns: character.name, actor.name
  SELECT character.name, actor.name
  FROM character
  LEFT JOIN character_actor
  ON character.id = character_actor.character_id
  LEFT JOIN actor
  ON character_actor.actor_id = actor.id;

  SELECT c.name, a.name
  FROM character AS c
  LEFT JOIN character_actor AS ca
  ON c.id = ca.character_id
  LEFT JOIN actor AS a
  ON ca.actor_id = a.id;

##Can you run a query that returns the name of an employee and the name of their boss? Use column aliases to make the columns employee_name and boss_name.
  SELECT e.name AS employee_name, b.name AS boss_name
  FROM employees AS e
  INNER JOIN employees as b
  ON e.boss_id = b.id

Can you return the results with a column named sound that returns "talk" for humans, "bark" for dogs, and "meow" for cats?
  SELECT *, 
  CASE WHEN species = 'human' THEN 'talk'
  WHEN species = 'dog' THEN 'bark'
  WHEN species = 'cat' THEN 'meow'
  END
  AS sound
  FROM friends_of_pickles;
