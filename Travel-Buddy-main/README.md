Create a databased named users.db and modify the location specifiacation line for the database in app.py(line 16).
Create the following database in users.db(use DB Browser):
CREATE TABLE "user" (
	"id"	INTEGER NOT NULL,
	"username"	VARCHAR(80) NOT NULL,
	"password"	VARCHAR(120) NOT NULL,
	"achievements"	INTEGER DEFAULT 0,
	"travel_points"	INTEGER DEFAULT 0,
	"places"	INTEGER DEFAULT 0,
	"rank"	INTEGER,
	PRIMARY KEY("id"),
	UNIQUE("username")
);

Also create the following triggers:
1)CREATE TRIGGER update1_user_ranks
AFTER UPDATE ON "user"
BEGIN
    UPDATE "user"
    SET rank = (
        SELECT COUNT(*) + 1 
        FROM "user" AS u
        WHERE u.travel_points > "user".travel_points
    );
END

2)CREATE TRIGGER update_user_ranks
AFTER INSERT ON "user"
BEGIN
    UPDATE "user"
    SET rank = (
        SELECT COUNT(*) + 1 
        FROM "user" AS u
        WHERE u.travel_points > "user".travel_points
    );
END
