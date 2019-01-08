
# Table of Contents
1. [HBase Client](#HBase-Client)
2. [Java Sample Code](#Java-Sample-Code)
3. [Flink ](#Flink)







#### HBase Client

```

import java.io.IOException;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class TableExists{

   public static void main(String args[])throws IOException{

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Verifying the existance of the table
      boolean bool = admin.tableExists("emp");
      System.out.println( bool);
   }
} 

admin.deleteTable("emp12");
admin.disableTable("emp1");



Configuration config = HBaseConfiguration.create();
config.addResource("hbase-site.xml");
try{
   Connection connection = 
   ConnectionFactory.createConnection(config);
   Table table = connection.getTable(TableName.valueOf("tableName"));
   Get getVal = new Get(Bytes.toBytes("rowkey"));
   Result result = table.get(getVal);
   byte [] value = 
   result.getValue(Bytes.toBytes("cf"),Bytes.toBytes("dataCol"));
}

Shut down the HBase using the shutdown() method of the HBaseAdmin class.

admin.shutdown();

HBase is written in Java and has a Java Native API. Therefore it provides programmatic access to Data Manipulation Language (DML).

Class HTable
HTable is an HBase internal class that represents an HBase table. It is an implementation of table that is used to communicate with a single HBase table. This class belongs to the org.apache.hadoop.hbase.client class.

Constructors
S.No.	Constructors and Description
1	HTable()

2	HTable(TableName tableName, ClusterConnection connection, ExecutorService pool)

Using this constructor, you can create an object to access an HBase table.


1	void close() Releases all the resources of the HTable.

2	void delete(Delete delete) Deletes the specified cells/row.

3	boolean exists(Get get) Using this method, you can test the existence of columns in the table, as specified by Get.

4	Result get(Get get) Retrieves certain cells from a given row.

5	org.apache.hadoop.conf.Configuration getConfiguration()	Returns the Configuration object used by this instance.

6	TableName getName() 	Returns the table name instance of this table.

7	HTableDescriptor getTableDescriptor()	Returns the table descriptor for this table.

8	byte[] getTableName()	Returns the name of this table.

9	void put(Put put)		Using this method, you can insert data into the table.


---------------------------------------------------------------------------------------------------

```
public class ScanTable{

   public static void main(String args[]) throws IOException{
      // Instantiating Configuration class
      Configuration config = HBaseConfiguration.create();
      // Instantiating HTable class
      HTable table = new HTable(config, "emp");
      // Instantiating the Scan class
      Scan scan = new Scan();
      // Scanning the required columns
      scan.addColumn(Bytes.toBytes("personal"), Bytes.toBytes("name"));
      scan.addColumn(Bytes.toBytes("personal"), Bytes.toBytes("city"));
      // Getting the scan result
      ResultScanner scanner = table.getScanner(scan);
      // Reading values from scan result
      for (Result result = scanner.next(); result != null; result = scanner.next())
      System.out.println("Found row : " + result);
      //closing the scanner
      scanner.close();
   }
}

```

`Inset into table`


import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Connection;
import org.apache.hadoop.hbase.client.ConnectionFactory;
import org.apache.hadoop.hbase.client.Put;
import org.apache.hadoop.hbase.client.Table;
import org.apache.hadoop.hbase.util.Bytes;
 

public class InsertIntoTable {
 
    public static void main(String[] args) {
        InsertIntoTable object = new InsertIntoTable();
        object.insertRecords();
    }
 
    public void insertRecords() {
         Configuration config = HBaseConfiguration.create();
         config.set("hbase.zookeeper.quorum", "127.0.0.1");
         config.set("hbase.zookeeper.property.clientPort", "2181");
 
         String tableName = "users";
 
         Connection connection = null;
         Table table = null;
 
         try {
            connection = ConnectionFactory.createConnection(config);
            table = connection.getTable(TableName.valueOf(tableName));
 
            //    creating sample data that can be used to save into hbase table
            String[][] people = {
			
                    { "1", "Marcel", "Haddad", "marcel@xyz.com", "M", "26" },
                    { "2", "Franklin", "Holtz", "franklin@xyz.com", "M", "24" },
                    { "3", "Dwayne", "McKee", "dwayne@xyz.com", "M", "27" },
                    { "4", "Rae", "Schroeder", "rae@xyz.com", "F", "31" },
                    { "5", "Rosalie", "burton", "rosalie@xyz.com", "F", "25" },
                    { "6", "Gabriela", "Ingram", "gabriela@xyz.com", "F", "24" } 
					
					};
 
            for (int i = 0; i < people.length; i++) {
			
                Put person = new Put(Bytes.toBytes(people[i][0]));
				
                person.addColumn(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
                person.addColumn(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
                person.addColumn(Bytes.toBytes("contact_info"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
                person.addColumn(Bytes.toBytes("personal_info"), Bytes.toBytes("gender"), Bytes.toBytes(people[i][4]));
                person.addColumn(Bytes.toBytes("personal_info"), Bytes.toBytes("age"), Bytes.toBytes(people[i][5]));
                table.put(person);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (table != null) {
                    table.close();
                }
 
                if (connection != null && !connection.isClosed()) {
                    connection.close();
                }
            } catch (Exception e2) {
                e2.printStackTrace();
            }
        }
    }
}



 
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Connection;
import org.apache.hadoop.hbase.client.ConnectionFactory;
 
/**
*
*
*/
public class CreateTable {
 
    public static void main(String[] args) {
        CreateTable object = new CreateTable();
        object.createTable();
    }
 
    public void createTable() {
        Configuration config = HBaseConfiguration.create();
        config.set("hbase.zookeeper.quorum", "127.0.0.1");
        config.set("hbase.zookeeper.property.clientPort", "2181");
 
        Connection connection = null;
        Admin admin = null;
 
        try {
            connection = ConnectionFactory.createConnection(config);
            admin = connection.getAdmin();
 
            String tableName = "users";
 
            if (!admin.isTableAvailable(TableName.valueOf(tableName))) {
                HTableDescriptor hbaseTable = new HTableDescriptor(TableName.valueOf(tableName));
                hbaseTable.addFamily(new HColumnDescriptor("name"));
                hbaseTable.addFamily(new HColumnDescriptor("contact_info"));
                hbaseTable.addFamily(new HColumnDescriptor("personal_info"));
                admin.createTable(hbaseTable);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (admin != null) {
                    admin.close();
                }
 
                if (connection != null && !connection.isClosed()) {
                    connection.close();
                }
            } catch (Exception e2) {
                e2.printStackTrace();
            }
        }
    }
}
}
```

## Java Sample Code


### Java File Read 

```
public void listFilesForFolder(final File folder) {
    for (final File fileEntry : folder.listFiles()) {
        if (fileEntry.isDirectory()) {
            listFilesForFolder(fileEntry);
        } else {
            System.out.println(fileEntry.getName());
        }
    }
}

final File folder = new File("/home/you/Desktop");
listFilesForFolder(folder);
Files.walk API is available from Java 8.

try (Stream<Path> paths = Files.walk(Paths.get("/home/you/Desktop"))) {
    paths
        .filter(Files::isRegularFile)
        .forEach(System.out::println);
} 

```


### HDFS Code Sample 

```

https://blog.matthewrathbone.com/2013/12/28/reading-data-from-hdfs-even-if-it-is-compressed

public List<String> readLines(Path location, Configuration conf) throws Exception {
    FileSystem fileSystem = FileSystem.get(location.toUri(), conf);
    CompressionCodecFactory factory = new CompressionCodecFactory(conf);
    FileStatus[] items = fileSystem.listStatus(location);
    if (items == null) return new ArrayList<String>();
    List<String> results = new ArrayList<String>();
    for(FileStatus item: items) {

      // ignoring files like _SUCCESS
      if(item.getPath().getName().startsWith("_")) {
        continue;
      }

      CompressionCodec codec = factory.getCodec(item.getPath());
      InputStream stream = null;

      // check if we have a compression codec we need to use
      if (codec != null) {
        stream = codec.createInputStream(fileSystem.open(item.getPath()));
      }
      else {
        stream = fileSystem.open(item.getPath());
      }

      StringWriter writer = new StringWriter();
      IOUtils.copy(stream, writer, "UTF-8");
      String raw = writer.toString();
      String[] resulting = raw.split("\n");
      for(String str: raw.split("\n")) {
        results.add(str);
      }
    }
    return results;
  }

// example usage:
Path myfile = new Path("/path/to/results.txt");
List<String> results = readLines(myfile, new Configuration());


public <A extends Writable, B extends Writable> List<Tuple<A, B>> readSequenceFile(Path path, Configuration conf, Class<A> acls, Class<B> bcls) throws Exception {
    
    SequenceFile.Reader reader = new SequenceFile.Reader(conf, SequenceFile.Reader.file(path));
    long position = reader.getPosition();

    A key = acls.newInstance();
    B value = bcls.newInstance();

    List<Tuple<A, B>> results = new ArrayList<Tuple<A,B>>();
    while(reader.next(key,value)) {
      results.add(new Tuple(key, value));
      key = acls.newInstance();
      value = bcls.newInstance();
    }
    return results;
  }

// example usage
List<Tuple<LongWritable, Text>> results = readSequenceFile(new Path("/a/b/c"), new Configuration(), LongWritable.class, Text.class);

https://community.hortonworks.com/articles/56702/a-secure-hdfs-client-example.html
Configuration conf = new Configuration();
conf.set("fs.defaultFS","hdfs://one.hdp:8020");
FileSystem fs = FileSystem.get(conf);
FileStatus[] fsStatus = fs.listStatus(new Path("/"));



Read Write
https://stackoverflow.com/questions/17564074/accessing-files-in-hdfs-using-java


https://tutorials.techmytalk.com/2014/08/16/hadoop-hdfs-java-api/

FileSystem file = FileSystem.get (uri, conf);
        FSDataInputStream in = file.open(new Path(uri));
        byte[] btbuffer = new byte[5];
        in.seek(5); // sent to 5th position
        Assert.assertEquals(5, in.getPos());
        in.read(btbuffer, 0, 5);//read 5 byte in byte array from offset 0
        System.out.println(new String(btbuffer));// &amp;amp;amp;quot; print 5 character from 5th position
      in.read(10,btbuffer, 0, 5);// print 5 character staring from 10th position


----------------
`Word Count program in Hadoop`

https://acadgild.com/blog/building-a-hadoop-application-using-maven

import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
public class WordCount {
  public static class TokenizerMapper
       extends Mapper<Object, Text, Text, IntWritable>{
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();
    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
      StringTokenizer itr = new StringTokenizer(value.toString());
      while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
      }
    }
  }
  public static class IntSumReducer
       extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();
    public void reduce(Text key, Iterable<IntWritable> values,
                       Context context
                       ) throws IOException, InterruptedException {
      int sum = 0;
      for (IntWritable val : values) {
        sum += val.get();
      }
      result.set(sum);
      context.write(key, result);
    }
  }
  public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    Job job = Job.getInstance(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
  }
}

File Read in HDFS 

import java.io.IOException;
import java.io.InputStream;
import java.net.URI;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IOUtils;

public class HadoopMain {

	public static void main(String[] args) {

		String uri = "hdfs://localhost:1234/home/hadoop/hadoop_store/input/catalogFile.csv";
		InputStream in = null;
		Configuration conf = new Configuration();
		try {
			FileSystem fs = FileSystem.get(URI.create(uri), conf);
			in = fs.open(new Path(uri));
			IOUtils.copyBytes(in, System.out, 4096, false);
		} catch (IOException e) {
			System.out.println("-------------------------->24");
			e.printStackTrace();
		} finally {
			IOUtils.closeStream(in);
		}

	}

}
	  
Refrences:
	  
http://www.allprogrammingtutorials.com/tutorials/reading-writing-files-in-hdfs-using-java-api.php	  
https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html
https://hadoop.apache.org/docs/r0.23.11/hadoop-project-dist/hadoop-common/CommandsManual.html	Hadoop Commands
https://dzone.com/articles/top-10-hadoop-shell-commands
https://www.edureka.co/blog/hadoop-cluster-configuration-files/	
https://creativedata.atlassian.net/wiki/spaces/SAP/pages/52199514/Java+-+Read+Write+files+with+HDFS
https://blog.cloudera.com/blog/2015/02/couchdoop-couchbase-meets-apache-hadoop/
}
```

## Flink 
1. Installation 

- Windows

- Linux

2. Maven Starter Project

> mvn archetype:generate -DarchetypeGroupId=org.apache.flink -DarchetypeArtifactId=flink-quickstart-java -DarchetypeVersion=1.6.3

3. First Program in Flink 
- https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html


**Other Use Case**




**Refrences**

- https://dzone.com/articles/getting-started-with-batch-processing-using-apache 
- https://ci.apache.org/projects/flink/flink-docs-stable/ops/filesystems.html	  
- https://brewing.codes/2017/10/01/start-flink-batch/
- https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html-  	  
- https://data-flair.training/forums/topic/in-which-location-namenode-stores-its-metadata-and-why/	  
- https://www.oreilly.com/library/view/stream-processing-with/9781491974285/ch04.html
- https://www.baeldung.com/apache-flink
- https://www.programcreek.com/java-api-examples/index.php?source_dir=flink-master/flink-runtime/src/main/java/org/apache/flink/runtime/fs/hdfs/HadoopFileSystem.java








