# AndSes4Ass3
Main Activity.java
package me.rk.andses4ass3;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.GridView;

public class MainActivity extends AppCompatActivity {

    Button gridView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        gridView=(Button) findViewById(R.id.gridview);
        gridView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, GridView1.class);
                startActivity(intent);
            }
        });
    }
}


GridView1.java
package me.rk.andses4ass3;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.widget.GridView;

/**
 * Created by airodyra on 6/19/2016.
 */
public class GridView1 extends Activity{

    private GridView mgridView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.grid_view_layout);

        mgridView=(GridView)findViewById(R.id.grid);


        final String[] nameArray={"GingerBread", "Honeycomb", "IceCream", "JellyBean", "KitKat", "Lollypop"};
        final int[] imagesArray={R.mipmap.gingerbread, R.mipmap.honeycomb, R.mipmap.icecream,
                R.mipmap.jellybean, R.mipmap.kitkat, R.mipmap.lollypop};


        CustomAdapter customAdapter=new CustomAdapter(GridView1.this, nameArray, imagesArray);
        mgridView.setAdapter(customAdapter);
    }
}

CustomAdapter.java
package me.rk.andses4ass3;

import android.content.Context;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ImageView;
import android.widget.TextView;

/**
 * Created by airodyra on 6/19/2016.
 */
public class CustomAdapter extends BaseAdapter{
    private Context mContext;
    private String[] mName;
    private int[] mimages;

    public CustomAdapter(Context context, String[]strings,int[]images){
        mContext=context;
        mName=strings;
        mimages=images;
    }
    @Override
    public int getCount() {
        return mimages.length;
    }

    @Override
    public Object getItem(int position) {
        return position;
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    public class ViewHolder{
        TextView nameTextView;
        ImageView imageView;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder viewHolder;

        if (convertView==null) {

            viewHolder=new ViewHolder();
            View rootView= View.inflate(mContext, R.layout.custom_list_layout, null);
            viewHolder.nameTextView = (TextView) rootView.findViewById(R.id.textView);
            viewHolder.imageView = (ImageView) rootView.findViewById(R.id.imageView);

            rootView.setTag(viewHolder);
            convertView=rootView;
        }

        else {
            viewHolder = (ViewHolder) convertView.getTag();
        }

        viewHolder.imageView.setImageResource(mimages[position]);
        viewHolder.nameTextView.setText(mName[position]);
        return convertView;
    }
}

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="me.rk.andses4ass3.MainActivity">

    <Button
        android:id="@+id/gridview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Grid View"
        android:textSize="24dp"
        android:layout_centerHorizontal="true"/>
</RelativeLayout>

grid_view_layout.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">


    <GridView
        android:id="@+id/grid"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:numColumns="auto_fit"
        android:verticalSpacing="10dp"
        android:horizontalSpacing="10dp"
        android:stretchMode="columnWidth"

        ></GridView>
</LinearLayout>

custom_list_layout.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@android:color/darker_gray">

    <ImageView
        android:id="@+id/imageView"
        android:layout_margin="10dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="@mipmap/jellybean"/>

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="19sp"
        android:layout_marginTop="20dp"
        android:textColor="#000000"
        android:text="Image1"/>

</LinearLayout>
