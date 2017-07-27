# How to get and parse a JSON file from URL

Just save some problem I solved when I'm doing my project.

Need to get a `JSON` file from `OpenWeatehrMAP` and get the description as well as temperature.

There is a easy way to do that. Need org.json.

The code:

``` Java
	private static String readAll(Reader rd) throws IOException {
		StringBuilder sb = new StringBuilder();
		int cp;
		while ((cp = rd.read()) != -1) {
			sb.append((char) cp);
			}
			return sb.toString();
		  }
          
```

``` Java

	public static JSONObject readJsonFromUrl(String url) throws IOException, JSONException {
		InputStream is = new URL(url).openStream();
		try {
			BufferedReader rd = new BufferedReader(new InputStreamReader(is, Charset.forName("UTF-8")));
			String jsonText = readAll(rd);
			JSONObject json = new JSONObject(jsonText);
			return json;
			} finally {
		      is.close();
		    }
		  }
 ```
 
 ``` Java
 	public String getweather() throws JSONException, IOException {
		String url = "……";
	    JSONObject json = readJsonFromUrl(url);
	    String description = json.getJSONArray("weather").getJSONObject(0).get("description").toString();
	    String temp_min = json.getJSONObject("main").get("temp_min").toString();
	    String temp_max = json.getJSONObject("main").get("temp_max").toString();
	    String temp = json.getJSONObject("main").get("temp").toString();
	    
	    String weather = "Today's weather in Glasgow is "+description+". The maximum tempearture is "+temp_max+
				 "degree, the minimum tempearture is "+temp_min+"degree and the current tempearture is "+temp+"degree.";
	    return weather;
	}
```

This is a copy from stack overflow, if there is any problem please contact me.
