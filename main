import datetime
import pytz
import random
import os
import pandas as pd
import safe_flower_functions as func 
import safe_flower_class as sfc



time_zone = pytz.timezone("Europe/Moscow")
date = datetime.datetime(2020, 5, 8, 12, 0, 0, 0, time_zone)
'''date = datetime.datetime.now(datetime.timezone.utc)'''


latitude = 57.57
longitude = 37.37
number_of_clouds = 30
cloud_list = list()


for i in range(number_of_clouds):

    center_of_cloud_x = random.randint(-150, 150)
    center_of_cloud_y = random.randint(-150, 150)
    height_cloud = random.randint(50, 150)
    speed_x = random.randint(-10, 10)
    speed_y = random.randint(-10, 10)
    const_x = random.randint(10, 40)
    const_y = random.randint(10, 40)
    cloud_list.append(sfc.Cloud(center_of_cloud_x, center_of_cloud_y, height_cloud, speed_x, speed_y, const_x, const_y))


flower = sfc.Flower(x0=0, y0=0, z0=0) # point of flower
lamp = sfc.Lamp()
lamp_zero_status = lamp.test() 

work_time = list()
status = list()



number_of_simulated_hours = 1 # how much hours you want


for t in range(number_of_simulated_hours*60): # hours -> minutes

    checking = list()
    sun = sfc.Sun(latitude, longitude, date)
    work_time.append(date.strftime("%Y-%m-%d-%H:%M"))

    for i in range(number_of_clouds):

        cloud = cloud_list[i]

        if func.check(sun, cloud, flower) or sun.vec()[2] < 0:

            checking.append(True)

        else:

            checking.append(False)

    if True in checking:

        lamp.on()   # choice of working mode

    else:

        lamp.off()

    func.plotting(sun, cloud_list, flower, t,number_of_clouds)  
    status.append(lamp.test())
    lamp_curr_status = lamp.test()

   
    lamp_zero_status = lamp_curr_status

    func.update_field(cloud_list, sun,number_of_clouds)
    date += datetime.timedelta(minutes=1)
func.simulation(number_of_simulated_hours)
os.startfile("Simulation.mp4")
df = pd.DataFrame({'Time since start': work_time, 'Lamp Status': status})
df.to_excel('CHECK_LIST.xlsx')
func.path_clear()
