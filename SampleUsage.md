# Introduction #

The all common operation of this library is available through static methods of DiffUtils object. These methods are:

  * `DiffUtils.diff(List<?> original, List<?>  revised): Patch patch`
  * `DiffUtils.patch(List<?> original, Patch patch): List<?> revised`
  * `DiffUtils.unpatch(List<?> revised, Patch patch): List<?> original`
  * `DiffUtils.parseUnifiedDiff(List<String> diff): Patch patch`
  * `DiffUtils.getDiffRows(List<String> original, List<String> revised): List<DiffRow> diffRows`

NOTE: All up-to-date examples can be found [here](http://code.google.com/p/java-diff-utils/source/browse/#svn%2Ftrunk%2Ftest%2Fexamples%2Fdiffutils).

### Basic use in a Java App ###

## Task 1: Compute the difference between to files and print its deltas ##

**Solution:**

```
import difflib.*;
 
public class BasicJavaApp_Task1 {
        // Helper method for get the file content
	private static List<String> fileToLines(String filename) {
		List<String> lines = new LinkedList<String>();
		String line = "";
		try {
			BufferedReader in = new BufferedReader(new FileReader(filename));
			while ((line = in.readLine()) != null) {
				lines.add(line);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
		return lines;
	}

	public static void main(String[] args) {
                List<String> original = fileToLines("originalFile.txt");
                List<String> revised  = fileToLines("revisedFile.xt");
                
                // Compute diff. Get the Patch object. Patch is the container for computed deltas.
                Patch patch = DiffUtils.diff(original, revised);

                for (Delta delta: patch.getDeltas()) {
                	System.out.println(delta);
                }
	}
}
```


## Task 2: Get the file in unified format and apply it as the patch to given text ##

**Solution:**

```
import difflib.*;
 
public class BasicJavaApp_Task2 {
        private List<String> originalList = Arrays.asList("aaa", "bbb", "ccc");

        // Helper method for get the file content
	private List<String> fileToLines(String filename) {
		List<String> lines = new LinkedList<String>();
		String line = "";
		try {
			BufferedReader in = new BufferedReader(new FileReader(filename));
			while ((line = in.readLine()) != null) {
				lines.add(line);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
		return lines;
	}

	public static void main(String[] args) {
                // At first, parse the unified diff file and get the patch
		Patch patch = DiffUtils.parseUnifiedDiff(fileToLines("example.diff"));
                
                // Then apply the computed patch to the given text
                List result = DiffUtils.patch(original, patch);
                /// Or we can call patch.applyTo(original). There is no difference.
	}
}
```

## Task 3: Compute the difference between to texts and print it in human-readable side-by-side view ##

**Solution:**

_Coming soon..._