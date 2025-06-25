python -m lerobot.teleoperate \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem59700736791 \
    --robot.id=my_awesome_follower_arm \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30},
                top: {type: opencv, index_or_path: 1, width: 640, height: 480, fps: 30}, }" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem59710814551 \
    --teleop.id=my_awesome_leader_arm \
    --display_data=true


huggingface-cli login --token ${HUGGINGFACE_TOKEN} --add-to-git-credential

HF_USER=$(huggingface-cli whoami | head -n 1)
echo $HF_USER

python -m lerobot.record \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem59700736791 \
    --robot.id=my_awesome_follower_arm \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30},
                top: {type: opencv, index_or_path: 1, width: 640, height: 480, fps: 30}, }" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem59710814551 \
    --teleop.id=my_awesome_leader_arm \
    --display_data=true \
    --dataset.repo_id=${HF_USER}/record-test10 \
    --dataset.num_episodes=2 \
    --dataset.single_task="Test dataset"


python -m lerobot.record_bbox \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem59700736791 \
    --robot.id=my_awesome_follower_arm \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30},
                top: {type: opencv, index_or_path: 3, width: 1920, height: 1080, fps: 30}, }" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem59710814551 \
    --teleop.id=my_awesome_leader_arm \
    --display_data=true \
    --dataset.repo_id=${HF_USER}/record-test10 \
    --dataset.num_episodes=2 \
    --dataset.single_task="Test bbox dataset"
