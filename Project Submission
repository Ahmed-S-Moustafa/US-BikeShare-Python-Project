'''About this project: This project is about writing a code to import, explore and answer intersting questions using
Python and pandas and some interesting modules 
to explore  US bokeshare data for 3 cities Chicago, New York and Washington).
Let's get started, shall we!
'''

'''The code structure is provided by Udacity. I'll follow along their stucture as I'm still a newbie. '''

# Import necessary modules for the code
import time
import pandas as pd
import numpy  as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

# Define the needed lists for cities, months, and days
city_choices = ['chicago', 'new york city', 'washington']
month_choices = ['january', 'february', 'march', 'april', 'may', 'june', 'all']
day_choices = ['saturday', 'sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'all']

def get_filters():
    
    print('Hello there! Let\'s explore some US bikeshare data! Ready? Let\'s Go!')
    #1 get user input for city (chicago, new york city, washington).
    while True:
        print('\nSELECT A CITY FROM THE OPTIONS BELOW\n')

        for cty in range(len(city_choices)):
            print(str(cty+1) + ":", city_choices[cty])
        
        cityin = input('Input a number from 1 to 3: \n')

        try: 
            cityin = int(cityin)
        except: print("Not a Number")
        
        else:
            if cityin in range(1,4):
                cityin = city_choices[cityin-1]
                print(f'You have selected : {cityin}\n')
                break
            else:
                print('number out of range')

    #2 get user input for month (all, january, february, ... , june)
    while True:

        print('\nLETS SELECT THE MONTH(S)\n')

        for mnt in range(len(month_choices)):
            print(str(mnt+1) + ":" , month_choices[mnt])

        monthin = input('Input a number from 1 to 6 for a month and 7 for ALL...\n')
        
        try:
            monthin = int(monthin)
        except: print("Not Number!")
            
        else:
            if monthin in range(1,8):
                monthin = month_choices[monthin-1]
                print(f' You have selected : {monthin}\n')
                break
            else:
                print('Invalid Month input, please enter a valid option')

    #3 get user input for day of week (all, monday, tuesday, ... sunday)
    while True:
        
        print('\nLETS SELECT THE DAY(S)\n')

        for dy in range(len(day_choices)):
                print(str(dy+1) + ":" , day_choices[dy])
        
        dayin= input('Input a number from 1 to 7 to choose a day and 8 for ALL...\n')

        try:
            dayin =int(dayin)
        except: print("NOT Number")

        else:
            if dayin in range(1,9):
                dayin = day_choices[dayin-1]
                print(f'You have selected : {dayin}\n')
                break
            else:
                print('Hmm, seems you chose a number out of range')
    print(f'The data will be anaylzed on this selection: {cityin} for {monthin} for the {dayin} weekday.')
    return cityin, monthin.capitalize(), dayin.capitalize()
        

def load_data(cityin, monthin, dayin):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) cityin - name of the city to analyze
        (str) monthin - name of the month to filter by, or "all" to apply no month filter
        (str) dayin - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    # Loading the CSV File as a df
    df = pd.read_csv(CITY_DATA[cityin])
    
    #1 Remove the unnamed column to clean the data visually when printing the raw data for the user. 
    df.drop(columns=df.columns[0], axis=1, inplace=True)
                #print(df.head())
                #print(df.info()) Start time >> dtype: Object, need to change to datetime64

    #2 Change the Start time datatype from object to datetime64
    df['Start Time'] = pd.to_datetime(df['Start Time'])

        ## MONTH NAME ##
    #3.1 Create a new column in df called 'month' and extracted the month from the Start Time column.
    df['month'] = df['Start Time'].dt.month_name()  # be careful, names are capitalized in df!!

        ## WEEK NAME ##
    #3.2 Create a new column in df called 'day_of_week' and extracted the day of the week from the Start Time column.
    df['day_of_week'] = pd.to_datetime(df['Start Time'])
    # 3.3 Change numerical weekday to English name of weekday
    df['day_of_week'] = df['day_of_week'].dt.day_name('English')  #be careful, names are capitalizedin df! Raises an error if not addressed!

        ## HOUR ##
    #4 Create a new column in df called 'hour' and extracted the time(hour) from the Start Time column.
    df['hour'] = pd.to_datetime(df['Start Time'])
    df['hour'] = df['hour'].dt.strftime('%H')

    #5 Code the user's input so data can be filtered accordingly for analysis and viewing
    if monthin != 'All' and dayin != 'All':              # if user choose any specific month and day, capitalized the ALL here since the user input is capitalzied
        df = df[(df['month'] == monthin) & (df['day_of_week'] == dayin)]                   # the if loop will prompt to filter days by
        print(f'The Data will be filtered according to {monthin} month and the {dayin} weekday.')
    elif monthin == 'All' and dayin != 'All':               # this will filter by day, when all months are selected
        df = df[df['day_of_week'] == dayin]
        print(f'The Data will be filtered according to the {dayin} weekday only.')
    elif monthin != 'All' and dayin == 'All':              # this will filter by month, when all days are selected
        df = df[df['month'] == monthin]
        print(f'The Data will be filtered according to {monthin} month only.')
    else:                                           # condition: month in month_choices == 'all' and day in day_choices == 'all':
        pass
        
    #print(df.head())
    return df


def time_stats(df, monthin, dayin):
    """Displays statistics on the most frequent times of travel."""

    print('\n___Data Statistics: Most Frequent Times of Travel____\n')
    run_start = time.time()
  
    # display the most common month
    if monthin == 'All' and dayin == 'All':
        popular_month = df.month.mode()[0]
        popular_day = df['day_of_week'].mode()[0]
        print(f'The most popular day is: {popular_day}')
        print(f'The most popular month is: {popular_month}')
    else:
        pass
    
    # display the most common day of week
    popular_day = df['day_of_week'].mode()[0]

    # display the most common start hour
    popular_hour = df.hour.mode()[0]

    print(f'The most popular hour of the day is: {popular_hour}')
    print('-'*30)
    print("\nThis calculation took %s seconds." % (time.time() - run_start))
    print('-'*30)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""
    
    print('\n___Data Statistics: Most Popular Stations and Trip____\n')
    start_time = time.time()

    # display most commonly used start station
    start_station_mode = df['Start Station'].mode()[0]

    # display most commonly used end station
    end_station_mode = df['End Station'].mode()[0]

    # display most frequent combination of start station and end station trip
    combined_start_end = (df['Start Station'] + ' AND ' + df['End Station']).mode()[0]

    #Stats print-outs
    
    print(f'The most commonly used start station is: {start_station_mode}')
    print(f'The most commonly used end station is: {end_station_mode}')
    print(f'The most frequent combination of start station and end station trip is: {combined_start_end}')
    print('-'*30)
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*30)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\n___Data Statistics: Total and Average Trip Duration____\n')
    start_time = time.time()

    # display total travel time (in seconds) need to calculate per minutes ( /60) and hours (/3600)
    total_travel_time = df['Trip Duration'].sum()
    
    # display mean travel time
    avg_travel_time = df['Trip Duration'].mean()
    
    # Print-outs
    print('\n___Total and Average Trip Duration____\n'.title())
    print(f'The total travel time is: {total_travel_time} seconds')
    print(f'The average travel time is: {avg_travel_time} seconds')
    print('-'*30)
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*30)


def user_stats(df):
    '''Displays statistics of user and gender count if available.'''
    print('\n___Data Statistics: User Type Count & Gender____\n')

    start_time = time.time()
   
    # Display counts of user types
    user_subscriber = df['User Type'].value_counts()[0] 
    user_customer = df['User Type'].value_counts()[1]

    print(f'The Count of User types are as follows...User Type (count) : 1.Subscriber : {user_subscriber} and 2.Customer : {user_customer}')
    
    # Display counts of gender (Note: only available for NYC and Chicago)
    if 'Gender' not in df.columns:
        print('\nGender data is not available for this city!\n')
    else:
        gender_m = df['Gender'].value_counts()[0]
        gender_f = df['Gender'].value_counts()[1]

        print(f'The Gender Count is as follows M : {gender_m} & F : {gender_f}')   
    
    # Display earliest (oldest DOB), most recent (youngest DOB), and most common year of birth (Note: only available for NYC and Chicago)
    if 'Birth Year' not in df.columns:
        print('Birth Year information is not available for this city!')
    else:
        earliest_dob = df['Birth Year'].min()
        recent_dob = df['Birth Year'].max()
        mode_dob = df['Birth Year'].mode()[0]

        print(f"The Earliest Year of Birth is : {earliest_dob}")
        print(f"The Most Recent Year of Birth is : {recent_dob}")
        print(f"The Most Common Year of Birth is : {mode_dob}")
        
        #plt.hist(df['Birth Year'], range = (1980, 2005), bins=25)
        #plt.show()
    
    print('-'*30)
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*30)
        

def view_raw_data(df):
    '''Displays the raw data after the user chooses their filters in first step.'''
    r = 0
    while True:
        question = input("Would you like to view some of the sample data used in this project? Enter yes or no.\n")
        if question == 'no':
            break
        else:
            first_five_rows = df.iloc[r:r+5]
            #r += 5
            print(first_five_rows)
            print('********')
            while True:
                question_more = input("Would you like to see more? Enter yes or no.\n")
                if question_more == 'no':
                    return
            #break
                else:
                    r += 5
                    next_five = df.iloc[r:r+5]
                    print(next_five)
    return


def main():
    while True:
        cityin, monthin, dayin = get_filters()
        df = load_data(cityin, monthin, dayin)
        time_stats(df, monthin, dayin)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        view_raw_data(df)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break
if __name__ == '__main__':
    main()

# Ahmed Sayed Moustafa 2021
