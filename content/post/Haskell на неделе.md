{
    "date": "2016-01-03",
    "description": null,
    "draft": false,
    "id": 130,
    "image": null,
    "meta_title": null,
    "slug": "haskell-issue1",
    "tags": [
        "haskell"
    ],
    "title": "Haskell на неделе",
    "type": "post"
}


Что интересного я встретил на неделе:

* Изучение иностранных языков по технологии Learn languages through fiction - https://github.com/jekor/vocabulink
* Шелл на haskell - https://github.com/chrisdone/hell
* [hesh](https://github.com/jekor/hesh) - инструмент для удобного написания скриптов на haskell
Пример:

        # !/usr/bin/env hesh
        -- Backup a PostgreSQL database to an encrypted file.
        
        main = do
          args <- System.Environment.getArgs
          case args of
            [database] -> do
              today <- $(date +%Y-%m-%d)
              let file = database ++ "-" ++ today ++ ".sql.gpg"
              $(pg_dump $database) |> $(gpg -e -r $EMAIL) /> file
            _ -> do
              progName <- System.Environment.getProgName
              $(echo "Usage: $progName <database>") /> "/dev/stderr"
*  Практическое применение haskell - http://habrahabr.ru/post/272871/
* Приобрел пару книжек(кстати скидки на packtpub) - 
  1. Haskell Data Analysis Cookbook - Nishant Shukla
  2. Haskell Design Patterns - Ryan Lemmer
