## Description

Тестовый проект по чтению и записи в C* с использованием CQL.
За основу взят пример из Cassandra hadoop_cql3_word_count


## Run instructions

mvn package
dse hadoop jar cqlreader.jar com.peterservice.giraph.cql.cqlreader.WordCount output_reducer=cassandra input_mapper=native

# Итого 

Отработана запись и чтение в/из C* CF.