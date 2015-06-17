---
title: Chartholdr.io is live
date: 2015-06-06
tags: image placeholder, foundation, ruby on rails, brainstorm trust
category: hackathon
---

I remember the first time I stumbled across Placehold.it, a simple image placeholder that shows a gray image with text indicating the width and height of the image.
lorem!


Lorem ipsum dolor sit amet, consectetur adipisicing elit. Deleniti perferendis incidunt debitis excepturi soluta impedit aliquam eveniet a corporis iure obcaecati vitae, nemo porro minima explicabo reiciendis, minus earum temporibus.Lorem ipsum dolor sit amet, consectetur adipisicing elit. Pariatur ipsa ducimus eaque placeat, fugiat nesciunt doloribus odit distinctio expedita fugit aut sapiente, quod voluptate velit doloremque explicabo tempora obcaecati quisquam.
READMORE
![Chartholdr pie graph](http://chartholdr.io/pie/200){:height="200px" width="200px"}


Lorem ipsum dolor sit amet, consectetur adipisicing elit. Natus odit explicabo maxime quidem aliquid, nemo necessitatibus quis quisquam doloribus. Explicabo, impedit magnam perspiciatis tenetur quasi id praesentium esse, reprehenderit dolorem.


##How it works
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Officia ea fugiat eaque tempore, dicta sint. Deserunt officiis error dolorum quisquam autem inventore, illo ipsum voluptas repudiandae laborum perspiciatis illum, ea.

~~~
it "will be correct size" do
	pie_gen = Generator.new(Chart.new("pie", 400, 400))
	FastImage.size(pie_gen.get)[0].should == 400
	FastImage.size(pie_gen.get)[1].should == 400
	bar_gen = Generator.new(Chart.new("bar", 505, 500))
	FastImage.size(bar_gen.get)[0].should == 505
	FastImage.size(bar_gen.get)[1].should == 500
	line_gen = Generator.new(Chart.new("line", 700, 200))
	FastImage.size(line_gen.get)[0].should == 700
	FastImage.size(line_gen.get)[1].should == 200
end
~~~
{: .language-ruby}

##Challenges

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid accusantium eius deleniti minima consectetur neque, architecto praesentium ipsa maxime a reiciendis libero omnis, quos facilis temporibus ratione quibusdam facere cupiditate.

[1]:https://twitter.com/NoahTrust