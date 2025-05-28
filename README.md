# module-2-04
I was using a newer version of SQLAlchemy and my password was @.


from sqlalchemy import create_engine, text
from urllib.parse import quote  # Not 'parse'!


# URL-encode the password to avoid breaking the connection string
password = quote("p@ssword")


# Build connection string
cnxn_string = "postgresql+psycopg2://{username}:{pswd}@{host}:{port}/{database}"


engine = create_engine(cnxn_string.format(
    username="postgres",
    pswd=password,
    host="localhost",
    port=5432,
    database="sqlda"
))


# Try running a simple query
with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM customers LIMIT 2;"))
    rows = result.fetchall()


for row in rows:
    print(row)

 
