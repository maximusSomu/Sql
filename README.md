# Sql 
Q1 >  Find the 5 oldest users of the Instagram-

       SELECT * 
       FROM users
       ORDER BY created_at
        LIMIT 5;
  
Q2 >  Find the users who have never posted a single photo on Instagram-

          SELECT username
          FROM users
           LEFT JOIN photos
	        ON users.id=photos.user_id
          WHERE photos.id IS NULL;
          
Q3 >   Identify the winner of the contest and provide their details to the team: -

        SELECT 
        username,
	      photos.id,
        photos.image_url, 
         count(likes.user_id) AS total
        FROM photos
       INNER JOIN likes 
       ON likes.photo_id=photos.id
       INNER JOIN users
       ON photos.user_id = users.id
       GROUP BY photos.id 
       ORDER BY total DESC
       LIMIT 1;
Q4 >  Identify and suggest the top 5 most commonly used hashtags on the platform: -

          SELECT 
              tags.tag_name,
	        COUNT(*) AS total
            FROM photo_tags
           JOIN tags
           ON photo_tags.tag_id= tags.id
           GROUP BY tags.id
          ORDER BY total DESC
          LIMIT 5;
          
 Q5 >  5.What day of the week do most users register on? Provide insights on when to schedule an ad campaign
 
        SELECT 
        dayname(created_at) AS day,
        count(*) as total
         FROM users
        GROUP BY day
        ORDER BY total DESC

Q6 >  Provide how many times does average user posts on Instagram. 

           SELECT (SELECT COUNT(*)FROM photos)/(SELECT COUNT(*) FROM users) as avg;

7. Provide data on users (bots) who have liked every single photo on the site 

                    SELECT users.id,username, COUNT(users.id) As total_likes_by_user
                    FROM users
                    JOIN likes ON users.id = likes.user_id
                    GROUP BY users.id
                    HAVING total_likes_by_user = (SELECT COUNT(*) FROM photos);
