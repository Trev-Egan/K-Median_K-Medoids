function [membership, centres] = k_medoids(X, n_cluster)
% X: the data matrix, rows are data points and columns are features
% n_cluster: number of cluster

if n_cluster > 4
    disp ('You have set too many clusters.');
    disp ('Set the number of clusters to be 1-4.');
    disp ('The program and visualization allow for up to 4 clusters.');
    return;
end

% Initialize the figure
figure('position', [200, 200, 600, 500]);
    
% Get the number of data points and number of features
[n_sample, n_feat] = size(X); 

% n_sample is the number of data points
% n_feat is the number of features
% n_cluster is the number of clusters

% Randomly initialize the starting cluster centres.
rng('shuffle');

% selects random matrix value to be medoid
centres = datasample(X, n_cluster);

disp('Start K-means clustering ... ');

% Initialization:
% In the begining, all data points are in cluster 1
% The "old_membership" variable is an n_sample-by-1 matrix.
% It saves the cluster id that each data point belongs to.
% Again, in the begining, all data points are in cluster 1
old_membership = ones(n_sample, 1);

% Display the initial cluster membership for all datapoints
% and the initial cluster centres
show(X, old_membership, n_cluster, centres, 'Cluster centres initialized!');

while true
    
    % Calculate the Manhattan distances
    % between every data point and every cluster centre.
    
    distance = pdist2(X, centres, 'cityblock');
    
    % E step: Assign data points to closest clusters.
    % Specifically, for each data point, find closest 
    % cluster centre, and assign the data point
    % to that cluster.
    
    [~, membership] = min(distance, [], 2);
    
    %Show the result of the E step.
    show(X, membership, n_cluster, centres, 'E step finished: Datapoints re-assigned!')

    % M step: Update cluster centres based on the new assignment.
    
    j = 1;
    if j <= n_cluster
    [~, index] = mink(sum(pdist2(X(membership == j,:), X(membership == j,:),"cityblock")),1);
    n_medoid(:,:) = findIndex(index, X, n_cluster, j);
    end
    
   
    
  
        
    %Show the result of the M step.
    show(X, membership, n_cluster, centres, 'M step finished: Cluster centers updated!')
    
    % Stop if no more updates.
    if sum(membership ~= old_membership)==0
        show(X, membership, n_cluster, centres, 'Done! ');
        break;
    end
    
    old_membership = membership;
end

function show(X, c_pred, n_cluster, centres, txt)
    symbol = ['ro'; 'gp'; 'bd'; 'k^'; 'r*'];
    hold off;
        
    for i = 1:n_cluster
        marker = mod(i,5);
        if i > 4            
            disp('Total number of clusters exceeds 4, some symbols in the plot are reused!');
        end
        plot(X(c_pred==i, 1), X(c_pred==i, 2), symbol(marker,:));
        hold on;
        plot(centres(i, 1), centres(i, 2), symbol(marker,2), 'MarkerFaceColor',symbol(marker,1));
    end
    text(4.2, 5.4, txt);
    drawnow;
    
    %Pause some time here.
    %Used to show figure with enough time.
    %You can change the pause time.
    pause(0.5);
    
    function [] = optimize(X, index)
        dis = pdist2(X, index, 'cityblock'); %calculates distance between new center and datapoints
        [~, member] = min(dis, [], 2);
    end
end
     function [new_medoid, transfer] = findIndex(index, X, n_clusters, j)
    %Finds the medoid with the clostest distance to points in cluster
       transfer(:,:) = X(membership == j);
       new_medoid(:,:) = transfer(index, :);
   %At this point I ran out of time to comlete the assignment and submitted
   %what I had
    end

end