http://stackoverflow.com/questions/18199705/ruby-on-rails-how-to-get-the-current-week-and-loop-through-it-to-display-its-da


https://github.com/sachin87/week-of-month/blob/master/lib/modules/day.rb

Find age in rails(http://stackoverflow.com/questions/819263/get-persons-age-in-ruby)

def age(dob)
  now = Time.now.utc.to_date
  now.year - dob.year - ((now.month > dob.month || (now.month == dob.month && now.day >= dob.day)) ? 0 : 1)
end
